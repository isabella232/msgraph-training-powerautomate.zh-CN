---
ms.openlocfilehash: e05217bc33d1cce8bc86ad56a8bd43c4f6b4ef2a
ms.sourcegitcommit: 64947f11d367ffbebbafb700fdfdc20617275f35
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "48829629"
---
<!-- markdownlint-disable MD002 MD041 -->

在创建使用新连接器的流之前，请使用 [Microsoft Graph 资源管理器](https://developer.microsoft.com/graph/graph-explorer) 在 microsoft graph 中发现 JSON 批处理的一些功能和功能。

在浏览器中打开 [Microsoft Graph 资源管理器](https://developer.microsoft.com/graph/graph-explorer) 。 使用 Office 365 租户管理员帐户登录。 从 **示例查询** 中搜索 **批次** 。

在左侧菜单中选择 " **执行并行获取** 示例" 查询。 选择屏幕右上角的 " **运行查询** " 按钮。

![图浏览器中的 "示例查询" 选项卡的屏幕截图](./images/sample-queries.png)

示例批处理操作批处理三个 HTTP GET 请求，并向 Graph 终结点发出单个 HTTP POST `/v1.0/$batch` 。

```json
{
    "requests": [
        {
            "url": "/me?$select=displayName,jobTitle,userPrincipalName",
            "method": "GET",
            "id": "1"
        },
        {
            "url": "/me/messages?$filter=importance eq 'high'&$select=from,subject,receivedDateTime,bodyPreview",
            "method": "GET",
            "id": "2"
        },
        {
            "url": "/me/events",
            "method": "GET",
            "id": "3"
        }
    ]
}
```

返回的响应如下所示。 记下 Microsoft Graph 返回的响应的数组。 对批处理请求的响应可能以不同于 POST 中请求顺序的顺序出现。 `id`应使用属性将各个批次请求与特定批次响应关联。

> [!NOTE]
> 为了提高可读性，响应已被截断。

```json
{
  "responses": [
    {
      "id": "1",
      "status": 200,
      "headers": {...},
      "body": {...}
    },
    {
      "id": "3",
      "status": 200,
      "headers": {...},
      "body": {...}
    }
    {
      "id": "2",
      "status": 200,
      "headers": {...},
      "body": {...}
    }
  ]
}
```

每个响应都包含 `id` 、、 `status` `headers` 和 `body` 属性。 如果 `status` 请求的属性指示失败，则 `body` 包含从请求返回的任何错误消息。

若要确保请求的操作的顺序，可以使用 [dependsOn](https://docs.microsoft.com/graph/json-batching#sequencing-requests-with-the-dependson-property) 属性对单个请求进行排序。

除序列化和依赖项操作外，JSON 批处理还假定一个基路径，并执行相对路径中的请求。 每个批处理请求元素都 `/v1.0/$batch` `/beta/$batch` 按指定方式从或终结点执行。 由于 `/beta` 终结点可能返回可能不会在终结点中返回的其他输出，因此这可能会产生重大差异 `/v1.0` 。

例如，在 [Microsoft Graph 资源管理器](https://developer.microsoft.com/graph/graph-explorer)中执行以下两个查询。

1. `/v1.0/$batch`使用以下 url 查询终结点 `/me` () 的复制和粘贴请求。

```json
{
  "requests": [
    {
      "id": 1,
      "url": "/me",
      "method": "GET"
    }
  ]
}
```

![选择了 v1.0 的 Graph 浏览器中批查询的屏幕截图](./images/batch-v1.png)

现在，使用版本选择器下拉箭头更改为 `beta` 终结点，并执行完全相同的请求。

![图-浏览-4](./images/batch-beta.png)

返回的结果有何区别？ 尝试其他一些查询来确定一些差异。

除了和终结点的不同响应内容 `/v1.0` 之外 `/beta` ，在发出批处理请求以获得尚未授予的权限时，务必要了解可能存在的错误。 例如，下面是创建 OneNote 笔记本的批处理请求项。

```json
{
  "id": 1,
  "url": "/groups/65c5ecf9-3311-449c-9904-29a2c76b9a50/onenote/notebooks",
  "headers": {
    "Content-Type": "application/json"
  },
  "method": "POST",
  "body": {
    "displayName": "Meeting Notes"
  }
}
```

但是，如果尚未授予创建 OneNote 笔记本的权限，则会收到以下响应。 注意状态代码 `403 (Forbidden)` 和错误消息，指示提供的 OAuth 令牌不包括完成请求的操作所需的范围。

```json
{
  "responses": [
    {
      "id": "1",
      "status": 403,
      "headers": {
        "Cache-Control": "no-cache"
      },
      "body": {
        "error": {
          "code": "40004",
          "message": "The OAuth token provided does not have the necessary scopes to complete the request.
            Please make sure you are including one or more of the following scopes: Notes.ReadWrite.All,
            Notes.Read.All (you provided these scopes: Group.Read.All,Group.ReadWrite.All,User.Read,User.Read.All)",
          "innerError": {
            "request-id": "92d50317-aa06-4bd7-b908-c85ee4eff0e9",
            "date": "2018-10-17T02:01:10"
          }
        }
      }
    }
  ]
}
```

批处理中的每个请求将返回状态代码和结果或错误消息。 您必须处理每个响应，以便确定单个批处理操作是成功还是失败。

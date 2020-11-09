---
ms.openlocfilehash: 1674fb94e1749ad15f8f33f0865ce468f889232a
ms.sourcegitcommit: 64947f11d367ffbebbafb700fdfdc20617275f35
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "48829719"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="1fab2-101">在本练习中，将创建一个流，以使用您在前面的练习中创建的自定义连接器，以创建和配置 Microsoft 团队。</span><span class="sxs-lookup"><span data-stu-id="1fab2-101">In this exercise, you will create a flow to use the custom connector you created in previous exercises to create and configure a Microsoft Team.</span></span> <span data-ttu-id="1fab2-102">流将使用自定义连接器发送 POST 请求来创建 Office 365 统一组，在组创建完成时暂停延迟，然后发送 PUT 请求，将组与 Microsoft 团队相关联。</span><span class="sxs-lookup"><span data-stu-id="1fab2-102">The flow will use the custom connector to send a POST request to create an Office 365 Unified Group, will pause for a delay while the group creation completes, and then will send a PUT request to associate the group with a Microsoft Team.</span></span>

<span data-ttu-id="1fab2-103">在末尾，您的流看起来将类似于下图：</span><span class="sxs-lookup"><span data-stu-id="1fab2-103">In the end your flow will look similar to the following image:</span></span>

![已完成流的屏幕截图](./images/completed-flow.png)

<span data-ttu-id="1fab2-105">在浏览器中打开 [Microsoft Power 自动功能](https://flow.microsoft.com) ，并使用 Office 365 租户管理员帐户登录。</span><span class="sxs-lookup"><span data-stu-id="1fab2-105">Open [Microsoft Power Automate](https://flow.microsoft.com) in your browser and sign in with your Office 365 tenant administrator account.</span></span> <span data-ttu-id="1fab2-106">在左侧导航栏中选择 **"我的流** "。</span><span class="sxs-lookup"><span data-stu-id="1fab2-106">Choose **My flows** in the left-hand navigation.</span></span> <span data-ttu-id="1fab2-107">选择 " **新建** "，然后选择 " **即时-从空白** "。</span><span class="sxs-lookup"><span data-stu-id="1fab2-107">Choose **New** , then **Instant--from blank**.</span></span> <span data-ttu-id="1fab2-108">输入 `Create Team` **流名称** ，然后在 " **选择如何触发此流** " 下选择 " **手动触发流** "。</span><span class="sxs-lookup"><span data-stu-id="1fab2-108">Enter `Create Team` for **Flow name** , then select **Manually trigger a flow** under **Choose how to trigger this flow**.</span></span> <span data-ttu-id="1fab2-109">选择 **“创建”** 。</span><span class="sxs-lookup"><span data-stu-id="1fab2-109">Choose **Create**.</span></span>

<span data-ttu-id="1fab2-110">选择 " **手动触发流** 项目"，然后选择 " **添加输入** "，选择 " **文本** "，然后输入 `Name` 为 "标题"。</span><span class="sxs-lookup"><span data-stu-id="1fab2-110">Select the **Manually trigger a flow** item, then choose **Add an input** , select **Text** and enter `Name` as the title.</span></span>

![手动触发流触发器的屏幕截图](./images/manually-trigger.png)

<span data-ttu-id="1fab2-112">选择 " **新建步骤** "，然后 `Batch` 在搜索框中键入。</span><span class="sxs-lookup"><span data-stu-id="1fab2-112">Choose **New step** and type `Batch` in the search box.</span></span> <span data-ttu-id="1fab2-113">添加 **MS Graph 批处理连接器** 操作。</span><span class="sxs-lookup"><span data-stu-id="1fab2-113">Add the **MS Graph Batch Connector** action.</span></span> <span data-ttu-id="1fab2-114">选择省略号，并将此操作重命名为 `Batch POST-groups` 。</span><span class="sxs-lookup"><span data-stu-id="1fab2-114">Choose the ellipsis and rename this action to `Batch POST-groups`.</span></span>

<span data-ttu-id="1fab2-115">将以下代码添加到操作的 " **正文** " 文本框中。</span><span class="sxs-lookup"><span data-stu-id="1fab2-115">Add the following code into the **body** text box of the action.</span></span>

```json
{
  "requests": [
    {
      "url": "/groups",
      "method": "POST",
      "id": 1,
      "headers": { "Content-Type": "application/json" },
      "body": {
        "description": "REPLACE",
        "displayName": "REPLACE",
        "groupTypes": ["Unified"],
        "mailEnabled": true,
        "mailNickname": "REPLACE",
        "securityEnabled": false
      }
    }
  ]
}
```

<span data-ttu-id="1fab2-116">通过从 `REPLACE` `Name` " **添加动态内容** " 菜单中选择手动触发器中的值来替换每个占位符。</span><span class="sxs-lookup"><span data-stu-id="1fab2-116">Replace each `REPLACE` placeholder by selecting the `Name` value from the manual trigger from the **Add dynamic content** menu.</span></span>

![Microsoft Flow 中的 "动态内容" 菜单的屏幕截图](./images/dynamic-content.png)

<span data-ttu-id="1fab2-118">依次选择 " **新建步骤** "、"搜索 `delay` 和添加 **延迟** " 操作和 "配置为1分钟"。</span><span class="sxs-lookup"><span data-stu-id="1fab2-118">Choose **New step** , search for `delay` and add a **Delay** action and configure for 1 minute.</span></span>

<span data-ttu-id="1fab2-119">选择 " **新建步骤** "，然后 `Batch` 在搜索框中键入。</span><span class="sxs-lookup"><span data-stu-id="1fab2-119">Choose **New step** and type `Batch` in the search box.</span></span> <span data-ttu-id="1fab2-120">添加 **MS Graph 批处理连接器** 操作。</span><span class="sxs-lookup"><span data-stu-id="1fab2-120">Add the **MS Graph Batch Connector** action.</span></span> <span data-ttu-id="1fab2-121">选择省略号，并将此操作重命名为 `Batch PUT-team` 。</span><span class="sxs-lookup"><span data-stu-id="1fab2-121">Choose the ellipsis and rename this action to `Batch PUT-team`.</span></span>

<span data-ttu-id="1fab2-122">将以下代码添加到操作的 " **正文** " 文本框中。</span><span class="sxs-lookup"><span data-stu-id="1fab2-122">Add the following code into the **body** text box of the action.</span></span>

```json
{
  "requests": [
    {
      "id": 1,
      "url": "/groups/REPLACE/team",
      "method": "PUT",
      "headers": {
        "Content-Type": "application/json"
      },
      "body": {
        "memberSettings": {
          "allowCreateUpdateChannels": true
        },
        "messagingSettings": {
          "allowUserEditMessages": true,
          "allowUserDeleteMessages": true
        },
        "funSettings": {
          "allowGiphy": true,
          "giphyContentRating": "strict"
        }
      }
    }
  ]
}
```

<span data-ttu-id="1fab2-123">选择 `REPLACE` 占位符，然后选择 "动态内容" 窗格中的 " **表达式** "。</span><span class="sxs-lookup"><span data-stu-id="1fab2-123">Select the `REPLACE` placeholder, then select **Expression** in the dynamic content pane.</span></span> <span data-ttu-id="1fab2-124">将以下公式添加到 **表达式** 中。</span><span class="sxs-lookup"><span data-stu-id="1fab2-124">Add the following formula into the **Expression**.</span></span>

```js
body('Batch_POST-groups').responses[0].body.id
```

![动态内容窗格中的表达式的屏幕截图](./images/flow-formula.png)

<span data-ttu-id="1fab2-126">此公式指定我们希望从第一个操作的结果中使用组 ID。</span><span class="sxs-lookup"><span data-stu-id="1fab2-126">This formula specifies that we want to use the group ID from the result of the first action.</span></span>

![更新的操作正文的屏幕截图](./images/updated-body.png)

<span data-ttu-id="1fab2-128">选择 " **保存** "，然后选择 " **测试** " 以执行流。</span><span class="sxs-lookup"><span data-stu-id="1fab2-128">Choose **Save** , then choose **Test** to execute the flow.</span></span>

> [!TIP]
> <span data-ttu-id="1fab2-129">如果收到类似于的错误 `The template validation failed: 'The action(s) 'Batch_POST-groups' referenced by 'inputs' in action 'Batch_2' are not defined in the template'` ，表达式是错误的，并且可能引用了无法找到的流操作。</span><span class="sxs-lookup"><span data-stu-id="1fab2-129">If you receive an error like `The template validation failed: 'The action(s) 'Batch_POST-groups' referenced by 'inputs' in action 'Batch_2' are not defined in the template'`, the expression is incorrect and likely references a flow action it cannot find.</span></span> <span data-ttu-id="1fab2-130">确保要引用的操作名称完全匹配。</span><span class="sxs-lookup"><span data-stu-id="1fab2-130">Ensure that the action name you are referencing matches exactly.</span></span>

<span data-ttu-id="1fab2-131">选择 " **我将执行触发操作"** 单选按钮，然后选择 " **保存 & 测试** "。</span><span class="sxs-lookup"><span data-stu-id="1fab2-131">Choose the **I'll perform the trigger** action radio button and choose **Save & Test**.</span></span> <span data-ttu-id="1fab2-132">在对话框中选择 " **继续** "。</span><span class="sxs-lookup"><span data-stu-id="1fab2-132">Choose **Continue** in the dialog.</span></span> <span data-ttu-id="1fab2-133">提供一个不带空格的名称，然后选择 " **运行流** " 以创建一个团队。</span><span class="sxs-lookup"><span data-stu-id="1fab2-133">Provide a name without spaces, and choose **Run flow** to create a Team.</span></span>

!["运行流" 对话框的屏幕截图](./images/run-flow.png)

<span data-ttu-id="1fab2-135">最后，选择 "已 **完成** " 以查看活动日志。</span><span class="sxs-lookup"><span data-stu-id="1fab2-135">Finally, choose the **Done** to see the activity log.</span></span> <span data-ttu-id="1fab2-136">流完成后，你的 Office 365 组和团队已配置完毕。</span><span class="sxs-lookup"><span data-stu-id="1fab2-136">Once the flow completes, your Office 365 Group and Team have been configured.</span></span> <span data-ttu-id="1fab2-137">选择 "批处理" 操作项以查看 JSON 批处理调用的结果。</span><span class="sxs-lookup"><span data-stu-id="1fab2-137">Select the Batch action items to view the results of the JSON Batch calls.</span></span> <span data-ttu-id="1fab2-138">`outputs` `Batch PUT-team` 操作的状态201代码应为成功的团队关联，如下面的图像所示。</span><span class="sxs-lookup"><span data-stu-id="1fab2-138">The `outputs` of the `Batch PUT-team` action should have a status code of 201 for a successful Team association similar to the image below.</span></span>

![成功流活动日志的屏幕截图](./images/success.png)

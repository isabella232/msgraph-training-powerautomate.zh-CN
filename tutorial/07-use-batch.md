---
ms.openlocfilehash: 2d9b6e29a5ddc71b8f7b78b1e2fe035a8fdbddac
ms.sourcegitcommit: 64947f11d367ffbebbafb700fdfdc20617275f35
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "48829704"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="b0992-101">您在上一练习中创建的流使用 `$batch` API 对 Microsoft Graph 发出两个单独的请求。</span><span class="sxs-lookup"><span data-stu-id="b0992-101">The Flow you created in the previous exercise uses the `$batch` API to make two individual requests to the Microsoft Graph.</span></span> <span data-ttu-id="b0992-102">`$batch`通过这种方式调用终结点可提供一些优点和灵活性，但在一 `$batch` 次调用中执行对 Microsoft Graph 的多个请求时，终结点的真正威力也是如此 `$batch` 。</span><span class="sxs-lookup"><span data-stu-id="b0992-102">Calling the `$batch` endpoint this way provides some benefit and flexibility, but the true power of the `$batch` endpoint comes when executing multiple requests to Microsoft Graph in a single `$batch` call.</span></span> <span data-ttu-id="b0992-103">在本练习中，你将扩展创建统一组的示例，并将团队关联起来，以在一个请求中为团队创建多个默认通道 `$batch` 。</span><span class="sxs-lookup"><span data-stu-id="b0992-103">In this exercise, you will extend the example of creating a Unified Group and associating a Team to include creating multiple default Channels for the Team in a single `$batch` request.</span></span>

<span data-ttu-id="b0992-104">在浏览器中打开 [Microsoft Power 自动功能](https://flow.microsoft.com) ，并使用 Office 365 租户管理员帐户登录。</span><span class="sxs-lookup"><span data-stu-id="b0992-104">Open [Microsoft Power Automate](https://flow.microsoft.com) in your browser and sign in with your Office 365 tenant administrator account.</span></span> <span data-ttu-id="b0992-105">选择您在上一步中创建的流，然后选择 " **编辑** "。</span><span class="sxs-lookup"><span data-stu-id="b0992-105">Select the Flow you created in the previous step and choose **Edit**.</span></span>

<span data-ttu-id="b0992-106">选择 " **新建步骤** "，然后 `Batch` 在搜索框中键入。</span><span class="sxs-lookup"><span data-stu-id="b0992-106">Choose **New step** and type `Batch` in the search box.</span></span> <span data-ttu-id="b0992-107">添加 **MS Graph 批处理连接器** 操作。</span><span class="sxs-lookup"><span data-stu-id="b0992-107">Add the **MS Graph Batch Connector** action.</span></span> <span data-ttu-id="b0992-108">选择省略号，并将此操作重命名为 `Batch POST-channels` 。</span><span class="sxs-lookup"><span data-stu-id="b0992-108">Choose the ellipsis and rename this action to `Batch POST-channels`.</span></span>

<span data-ttu-id="b0992-109">将以下代码添加到操作的 " **正文** " 文本框中。</span><span class="sxs-lookup"><span data-stu-id="b0992-109">Add the following code into the **body** text box of the action.</span></span>

```json
{
  "requests": [
    {
      "id": 1,
      "url": "/teams/REPLACE/channels",
      "headers": {
        "Content-Type": "application/json"
      },
      "method": "POST",
      "body": {
        "displayName": "Marketing Collateral",
        "description": "Marketing collateral and documentation."
      }
    },
    {
      "id": 2,
      "dependsOn": [
        "1"
      ],
      "url": "/teams/REPLACE/channels",
      "headers": {
        "Content-Type": "application/json"
      },
      "method": "POST",
      "body": {
        "displayName": "Vendor Contracts",
        "description": "Vendor documents, contracts, agreements and schedules."
      }
    },
    {
      "id": 3,
      "dependsOn": [
        "2"
      ],
      "url": "/teams/REPLACE/channels",
      "headers": {
        "Content-Type": "application/json"
      },
      "method": "POST",
      "body": {
        "displayName": "General Client Agreements",
        "description": "General Client documents and agreements."
      }
    }
  ]
}
```

<span data-ttu-id="b0992-110">请注意，上面的三个请求使用 [dependsOn](https://docs.microsoft.com/graph/json-batching#sequencing-requests-with-the-dependson-property) 属性来指定一个序列顺序，每个请求都将执行一个 POST 请求，以在新团队中创建新的通道。</span><span class="sxs-lookup"><span data-stu-id="b0992-110">Notice the three requests above are using the [dependsOn](https://docs.microsoft.com/graph/json-batching#sequencing-requests-with-the-dependson-property) property to specify a sequence order, and each will execute a POST request to create a new channel in the new Team.</span></span>

<span data-ttu-id="b0992-111">选择占位符的每个实例 `REPLACE` ，然后选择 "动态内容" 窗格中的 " **表达式** "。</span><span class="sxs-lookup"><span data-stu-id="b0992-111">Select each instance of the `REPLACE` placeholder, then select **Expression** in the dynamic content pane.</span></span> <span data-ttu-id="b0992-112">将以下公式添加到 **表达式** 中。</span><span class="sxs-lookup"><span data-stu-id="b0992-112">Add the following formula into the **Expression**.</span></span>

```js
body('Batch_PUT-team').responses[0].body.id
```

![动态内容窗格中的表达式的屏幕截图](./images/dynamic-expression.png)

<span data-ttu-id="b0992-114">选择 " **保存** "，然后选择 " **测试** " 以执行流。</span><span class="sxs-lookup"><span data-stu-id="b0992-114">Choose **Save** , then choose **Test** to execute the Flow.</span></span> <span data-ttu-id="b0992-115">选择 " **我将执行触发操作"** 单选按钮，然后选择 " **保存 & 测试** "。</span><span class="sxs-lookup"><span data-stu-id="b0992-115">Select the **I'll perform the trigger** action radio button, then choose **Save & Test**.</span></span> <span data-ttu-id="b0992-116">在 " **名称** " 字段中输入一个不带空格的唯一组名称，然后选择 " **运行流** " 以执行流。</span><span class="sxs-lookup"><span data-stu-id="b0992-116">Enter a unique group name in the **Name** field without spaces, and choose **Run flow** to execute the Flow.</span></span>

<span data-ttu-id="b0992-117">流启动后，选择 " **完成** " 按钮以查看活动日志。</span><span class="sxs-lookup"><span data-stu-id="b0992-117">Once the Flow starts, choose the **Done** button to see the activity log.</span></span> <span data-ttu-id="b0992-118">在流完成后，对于创建的每个通道，该操作的最终输出 `Batch POST-channels` 都具有 201 HTTP 状态响应。</span><span class="sxs-lookup"><span data-stu-id="b0992-118">When the Flow completes, the final output for the `Batch POST-channels` action has a 201 HTTP Status response for each Channel created.</span></span>

![成功流活动日志的屏幕截图](./images/batch-success.png)

<span data-ttu-id="b0992-120">浏览到 [Microsoft 团队](https://teams.microsoft.com) ，并使用 Office 365 租户管理员帐户登录。</span><span class="sxs-lookup"><span data-stu-id="b0992-120">Browse to [Microsoft Teams](https://teams.microsoft.com) and sign in with your Office 365 tenant administrator account.</span></span> <span data-ttu-id="b0992-121">验证刚创建的团队是否显示并包含由请求创建的三个通道 `$batch` 。</span><span class="sxs-lookup"><span data-stu-id="b0992-121">Verify that the team you just created appears and includes the three channels created by the `$batch` request.</span></span>

![显示新团队和频道的团队应用程序的屏幕截图](./images/team-channels.png)

<span data-ttu-id="b0992-123">虽然 `Batch POST-channels` 在本教程中实施了上述操作作为一个单独的操作，但创建通道的调用可以作为操作中的其他调用添加 `Batch PUT-team` 。</span><span class="sxs-lookup"><span data-stu-id="b0992-123">While the above `Batch POST-channels` action was implemented in this tutorial as a separate action, the calls to create the channels could have been added as additional calls in the `Batch PUT-team` action.</span></span> <span data-ttu-id="b0992-124">这将在单个批次调用中创建团队和所有频道。</span><span class="sxs-lookup"><span data-stu-id="b0992-124">This would have created the Team and all Channels in a single batch call.</span></span> <span data-ttu-id="b0992-125">为此，请再试一试。</span><span class="sxs-lookup"><span data-stu-id="b0992-125">Give that a try on your own.</span></span>

<span data-ttu-id="b0992-126">最后，请记住， [JSON 批处理](https://docs.microsoft.com/graph/json-batching) 调用将为每个请求返回一个 HTTP 状态代码。</span><span class="sxs-lookup"><span data-stu-id="b0992-126">Finally, remember that [JSON Batching](https://docs.microsoft.com/graph/json-batching) calls will return an HTTP status code for each request.</span></span> <span data-ttu-id="b0992-127">在生产过程中，您可能希望将结果的后续处理与操作组合在一起 [`Apply to each`](https://docs.microsoft.com/power-automate/apply-to-each) ，并验证每个单独的响应是否有201状态代码或补偿收到的任何其他状态代码。</span><span class="sxs-lookup"><span data-stu-id="b0992-127">In a production process, you may want to combine post processing of the results with an [`Apply to each`](https://docs.microsoft.com/power-automate/apply-to-each) action and validate each individual response has a 201 status code or compensate for any other status codes received.</span></span>

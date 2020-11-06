---
ms.openlocfilehash: 24aac7ad8709fd70d87f1a2d0d0ceecf99aed2db
ms.sourcegitcommit: 64947f11d367ffbebbafb700fdfdc20617275f35
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "48829631"
---
# <a name="microsoft-graph-training-module---create-a-microsoft-graph-json-batch-custom-connector-for-microsoft-power-automate--azure-logic-apps"></a><span data-ttu-id="8847f-101">Microsoft Graph 培训模块-创建 Microsoft Graph JSON 批量自定义连接器，以实现 Microsoft Power & Azure 逻辑应用程序的自动化</span><span class="sxs-lookup"><span data-stu-id="8847f-101">Microsoft Graph Training Module - Create a Microsoft Graph JSON Batch Custom Connector for Microsoft Power Automate & Azure Logic Apps</span></span>

<span data-ttu-id="8847f-102">本模块将介绍如何使用 Microsoft Graph JSON 批处理 REST API 来访问 Office 365 中的数据。</span><span class="sxs-lookup"><span data-stu-id="8847f-102">This module will introduce you to working with the Microsoft Graph JSON Batching REST API to access data in Office 365.</span></span> <span data-ttu-id="8847f-103">您将了解如何创建和配置自定义连接器以实现 Microsoft Power 自动化，访问 Microsoft Graph JSON 批处理 API，并使用流中的自定义连接器创建 Microsoft 团队。</span><span class="sxs-lookup"><span data-stu-id="8847f-103">You will learn how to create and configure a custom connector for Microsoft Power Automate, access the the Microsoft Graph JSON Batch API, and use the custom connector in a flow to create a Microsoft Team.</span></span>

## <a name="lab---create-a-microsoft-graph-json-batch-custom-connector-for-microsoft-power-automate--azure-logic-apps"></a><span data-ttu-id="8847f-104">Lab-创建 Microsoft Graph JSON 批量自定义连接器，以实现 Microsoft Power & Azure 逻辑应用程序的自动化</span><span class="sxs-lookup"><span data-stu-id="8847f-104">Lab - Create a Microsoft Graph JSON Batch Custom Connector for Microsoft Power Automate & Azure Logic Apps</span></span>

<span data-ttu-id="8847f-105">在此实验室中，你将利用 Microsoft Graph JSON 批处理 REST API 创建自定义连接器和流应用程序。</span><span class="sxs-lookup"><span data-stu-id="8847f-105">In this lab you will leverage the Microsoft Graph JSON Batching REST API to create a Custom Connector and flow application.</span></span>

- [<span data-ttu-id="8847f-106">Microsoft Graph 教程的电源自动化</span><span class="sxs-lookup"><span data-stu-id="8847f-106">Power Automate Microsoft Graph tutorial</span></span>](https://docs.microsoft.com/graph/tutorials/powerautomate)

## <a name="contributors"></a><span data-ttu-id="8847f-107">参与者</span><span class="sxs-lookup"><span data-stu-id="8847f-107">Contributors</span></span>

| <span data-ttu-id="8847f-108">角色</span><span class="sxs-lookup"><span data-stu-id="8847f-108">Roles</span></span>       | <span data-ttu-id="8847f-109">Author (s) </span><span class="sxs-lookup"><span data-stu-id="8847f-109">Author(s)</span></span>                                            |
|-------------|------------------------------------------------------|
| <span data-ttu-id="8847f-110">实验室手册</span><span class="sxs-lookup"><span data-stu-id="8847f-110">Lab Manuals</span></span> | <span data-ttu-id="8847f-111">Microsoft MVP、SharePointGurus)  (John Liu @johnnliu</span><span class="sxs-lookup"><span data-stu-id="8847f-111">John Liu (Microsoft MVP, SharePointGurus) @johnnliu</span></span>  |
| <span data-ttu-id="8847f-112">实验室手册</span><span class="sxs-lookup"><span data-stu-id="8847f-112">Lab Manuals</span></span> | <span data-ttu-id="8847f-113">Pete Skelly (ThreeWill) @pskelly</span><span class="sxs-lookup"><span data-stu-id="8847f-113">Pete Skelly (ThreeWill) @pskelly</span></span>                     |
| <span data-ttu-id="8847f-114">实验室手册</span><span class="sxs-lookup"><span data-stu-id="8847f-114">Lab Manuals</span></span> | <span data-ttu-id="8847f-115">Ayca 营业活动 Bas (Microsoft) @aycabas</span><span class="sxs-lookup"><span data-stu-id="8847f-115">Ayca Bas (Microsoft) @aycabas</span></span>                        |

## <a name="version-history"></a><span data-ttu-id="8847f-116">版本历史记录</span><span class="sxs-lookup"><span data-stu-id="8847f-116">Version history</span></span>

| <span data-ttu-id="8847f-117">版本</span><span class="sxs-lookup"><span data-stu-id="8847f-117">Version</span></span> | <span data-ttu-id="8847f-118">日期</span><span class="sxs-lookup"><span data-stu-id="8847f-118">Date</span></span>              | <span data-ttu-id="8847f-119">注释</span><span class="sxs-lookup"><span data-stu-id="8847f-119">Comments</span></span>                                             |
|---------|-------------------|------------------------------------------------------|
| <span data-ttu-id="8847f-120">1.3</span><span class="sxs-lookup"><span data-stu-id="8847f-120">1.3</span></span>     | <span data-ttu-id="8847f-121">2020 年 8 月 24 日</span><span class="sxs-lookup"><span data-stu-id="8847f-121">August 24, 2020</span></span>   | <span data-ttu-id="8847f-122">更新以实现自动电源</span><span class="sxs-lookup"><span data-stu-id="8847f-122">Updated to Power Automate</span></span>                            |
| <span data-ttu-id="8847f-123">1.2</span><span class="sxs-lookup"><span data-stu-id="8847f-123">1.2</span></span>     | <span data-ttu-id="8847f-124">2018 年 11 月 27 日</span><span class="sxs-lookup"><span data-stu-id="8847f-124">November 27, 2018</span></span> | <span data-ttu-id="8847f-125">载入到 docs.microsoft.com/graph</span><span class="sxs-lookup"><span data-stu-id="8847f-125">Onboarded to docs.microsoft.com/graph</span></span>                |
| <span data-ttu-id="8847f-126">1.1</span><span class="sxs-lookup"><span data-stu-id="8847f-126">1.1</span></span>     | <span data-ttu-id="8847f-127">2007年11月，2018</span><span class="sxs-lookup"><span data-stu-id="8847f-127">November 07, 2018</span></span> | <span data-ttu-id="8847f-128">添加了用于调用多个操作的步骤6内容</span><span class="sxs-lookup"><span data-stu-id="8847f-128">Added step 6 content for calling multiple operations</span></span> |
| <span data-ttu-id="8847f-129">1.0</span><span class="sxs-lookup"><span data-stu-id="8847f-129">1.0</span></span>     | <span data-ttu-id="8847f-130">2018 年 10 月 22 日</span><span class="sxs-lookup"><span data-stu-id="8847f-130">October 22, 2018</span></span>  | <span data-ttu-id="8847f-131">添加与 Microsoft Graph 相关的产品 breakouts。</span><span class="sxs-lookup"><span data-stu-id="8847f-131">Add Microsoft Graph related product breakouts.</span></span>       |

## <a name="disclaimer"></a><span data-ttu-id="8847f-132">免责声明</span><span class="sxs-lookup"><span data-stu-id="8847f-132">Disclaimer</span></span>

<span data-ttu-id="8847f-133">**此代码 *按* 原样提供，无需任何明示或暗示的担保，包括对特定目的适用性、适销性或不侵权的任何暗示担保。**</span><span class="sxs-lookup"><span data-stu-id="8847f-133">**THIS CODE IS PROVIDED *AS IS* WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESS OR IMPLIED, INCLUDING ANY IMPLIED WARRANTIES OF FITNESS FOR A PARTICULAR PURPOSE, MERCHANTABILITY, OR NON-INFRINGEMENT.**</span></span>

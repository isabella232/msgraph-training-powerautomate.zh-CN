---
ms.openlocfilehash: 90462157024c529a1cf183230298fbf80813b8c9
ms.sourcegitcommit: 64947f11d367ffbebbafb700fdfdc20617275f35
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "48829698"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="c39c7-101">在本练习中，将创建一个新的自定义连接器，可在 Microsoft Power 自动化或 Azure 逻辑应用中使用。</span><span class="sxs-lookup"><span data-stu-id="c39c7-101">In this exercise, you will create a new custom connector which can be used in Microsoft Power Automate or in Azure Logic Apps.</span></span> <span data-ttu-id="c39c7-102">将使用 Microsoft Graph 终结点的正确路径预建 OpenAPI 定义文件 `$batch` ，并使用其他设置来启用简单导入。</span><span class="sxs-lookup"><span data-stu-id="c39c7-102">The OpenAPI definition file is prebuilt with the correct path for the Microsoft Graph `$batch` endpoint and additional settings to enable simple import.</span></span>

<span data-ttu-id="c39c7-103">有两个选项可用于创建 Microsoft Graph 的自定义连接器：</span><span class="sxs-lookup"><span data-stu-id="c39c7-103">There are two options to create a custom connector for Microsoft Graph:</span></span>

- <span data-ttu-id="c39c7-104">从空白创建</span><span class="sxs-lookup"><span data-stu-id="c39c7-104">Create from blank</span></span>
- <span data-ttu-id="c39c7-105">导入 OpenAPI 文件</span><span class="sxs-lookup"><span data-stu-id="c39c7-105">Import an OpenAPI file</span></span>

## <a name="option-1-create-custom-connector-from-blank-template"></a><span data-ttu-id="c39c7-106">选项1：根据空白模板创建自定义连接器</span><span class="sxs-lookup"><span data-stu-id="c39c7-106">Option 1: Create custom connector from blank template</span></span>

<span data-ttu-id="c39c7-107">打开浏览器并导航到 " [Microsoft Power 自动](https://flow.microsoft.com)"。</span><span class="sxs-lookup"><span data-stu-id="c39c7-107">Open a browser and navigate to [Microsoft Power Automate](https://flow.microsoft.com).</span></span> <span data-ttu-id="c39c7-108">使用 Office 365 租户管理员帐户登录。</span><span class="sxs-lookup"><span data-stu-id="c39c7-108">Sign in with your Office 365 tenant administrator account.</span></span> <span data-ttu-id="c39c7-109">选择左侧菜单中的 " **数据** "，然后在下拉菜单中选择 " **自定义连接器** " 项。</span><span class="sxs-lookup"><span data-stu-id="c39c7-109">Choose **Data** on the left-hand side menu, and select the **Custom Connectors** item in the drop-down menu.</span></span>

![Microsoft Power menu 中的下拉菜单的屏幕截图](./images/custom-connectors.png)

<span data-ttu-id="c39c7-111">在 " **自定义连接器** " 页上，选择右上方的 **新自定义连接线** 链接，然后从下拉菜单中选择 " **从空项创建** " 项。</span><span class="sxs-lookup"><span data-stu-id="c39c7-111">On the **Custom Connectors** page choose the **New custom connector** link in the top right, then select the **Create from blank** item in the drop-down menu.</span></span>

![Microsoft Power New 中的新自定义连接器下拉菜单的屏幕截图](./images/new-connector.png)

<span data-ttu-id="c39c7-113">`MS Graph Batch Connector`在 " **连接器名称** " 文本框中输入。</span><span class="sxs-lookup"><span data-stu-id="c39c7-113">Enter `MS Graph Batch Connector` in the **Connector name** text box.</span></span> <span data-ttu-id="c39c7-114">Choose **Continue**.</span><span class="sxs-lookup"><span data-stu-id="c39c7-114">Choose **Continue**.</span></span>

<span data-ttu-id="c39c7-115">在 "连接器配置 **常规** " 页上，按如下所示填写字段。</span><span class="sxs-lookup"><span data-stu-id="c39c7-115">On the connector configuration **General** page, fill in the fields as follows.</span></span>

- <span data-ttu-id="c39c7-116">**方案** ： HTTPS</span><span class="sxs-lookup"><span data-stu-id="c39c7-116">**Scheme** : HTTPS</span></span>
- <span data-ttu-id="c39c7-117">**主机** ： `graph.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="c39c7-117">**Host** : `graph.microsoft.com`</span></span>
- <span data-ttu-id="c39c7-118">**基 URL** ： `/`</span><span class="sxs-lookup"><span data-stu-id="c39c7-118">**Base URL** : `/`</span></span>

<span data-ttu-id="c39c7-119">选择 " **安全** " 按钮以继续。</span><span class="sxs-lookup"><span data-stu-id="c39c7-119">Choose **Security** button to continue.</span></span>

![连接器配置中的 "常规" 选项卡的屏幕截图](./images/general-tab.png)

<span data-ttu-id="c39c7-121">在 " **安全性** " 页上，按如下所示填写字段。</span><span class="sxs-lookup"><span data-stu-id="c39c7-121">On the **Security** page, fill in the fields as follows.</span></span>

- <span data-ttu-id="c39c7-122">**选择您的 API 实现的身份验证** ： `OAuth 2.0`</span><span class="sxs-lookup"><span data-stu-id="c39c7-122">**Choose what authentication is implemented by your API** : `OAuth 2.0`</span></span>
- <span data-ttu-id="c39c7-123">**标识提供程序** ： `Azure Active Directory`</span><span class="sxs-lookup"><span data-stu-id="c39c7-123">**Identity Provider** : `Azure Active Directory`</span></span>
- <span data-ttu-id="c39c7-124">**客户端 id** ：在上一练习中创建的应用程序 id</span><span class="sxs-lookup"><span data-stu-id="c39c7-124">**Client id** : the application ID you created in the previous exercise</span></span>
- <span data-ttu-id="c39c7-125">**客户端密码** ：在上一练习中创建的密钥</span><span class="sxs-lookup"><span data-stu-id="c39c7-125">**Client secret** : the key you created in the previous exercise</span></span>
- <span data-ttu-id="c39c7-126">**登录 url** ： `https://login.windows.net`</span><span class="sxs-lookup"><span data-stu-id="c39c7-126">**Login url** : `https://login.windows.net`</span></span>
- <span data-ttu-id="c39c7-127">**租户 ID** ： `common`</span><span class="sxs-lookup"><span data-stu-id="c39c7-127">**Tenant ID** : `common`</span></span>
- <span data-ttu-id="c39c7-128">**资源 URL** ： `https://graph.microsoft.com` (不带后缀/) </span><span class="sxs-lookup"><span data-stu-id="c39c7-128">**Resource URL** : `https://graph.microsoft.com` (no trailing /)</span></span>
- <span data-ttu-id="c39c7-129">**范围** ：保留为空</span><span class="sxs-lookup"><span data-stu-id="c39c7-129">**Scope** : Leave blank</span></span>

<span data-ttu-id="c39c7-130">选择 " **定义** " 按钮以继续。</span><span class="sxs-lookup"><span data-stu-id="c39c7-130">Choose **Definition** button to continue.</span></span>

![连接器配置中的 "安全" 选项卡的屏幕截图](./images/security-tab.png)

<span data-ttu-id="c39c7-132">在 " **定义** " 页上，选择 " **新建操作** "，并按如下所示填写字段。</span><span class="sxs-lookup"><span data-stu-id="c39c7-132">On the **Definition** page, select **New Action** and fill in the fields as follows.</span></span>

- <span data-ttu-id="c39c7-133">**摘要** ： `Batch`</span><span class="sxs-lookup"><span data-stu-id="c39c7-133">**Summary** : `Batch`</span></span>
- <span data-ttu-id="c39c7-134">**说明** ： `Execute Batch with Delegate Permission`</span><span class="sxs-lookup"><span data-stu-id="c39c7-134">**Description** : `Execute Batch with Delegate Permission`</span></span>
- <span data-ttu-id="c39c7-135">**操作 ID** ： `Batch`</span><span class="sxs-lookup"><span data-stu-id="c39c7-135">**Operation ID** : `Batch`</span></span>
- <span data-ttu-id="c39c7-136">**可见性** ： `important`</span><span class="sxs-lookup"><span data-stu-id="c39c7-136">**Visibility** : `important`</span></span>

![连接器配置中 "定义" 选项卡的屏幕截图](./images/definition-tab.png)

<span data-ttu-id="c39c7-138">通过选择 " **从示例导入** " 并填写字段中的 "创建 **请求** "，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c39c7-138">Create **Request** by selecting **Import from Sample** and fill in the fields as follows.</span></span>

- <span data-ttu-id="c39c7-139">**动词** ： `POST`</span><span class="sxs-lookup"><span data-stu-id="c39c7-139">**Verb** : `POST`</span></span>
- <span data-ttu-id="c39c7-140">**URL** : `https://graph.microsoft.com/v1.0/$batch`</span><span class="sxs-lookup"><span data-stu-id="c39c7-140">**URL** : `https://graph.microsoft.com/v1.0/$batch`</span></span>
- <span data-ttu-id="c39c7-141">**标头** ：保留为空</span><span class="sxs-lookup"><span data-stu-id="c39c7-141">**Headers** : Leave blank</span></span>
- <span data-ttu-id="c39c7-142">**正文** ： `{}`</span><span class="sxs-lookup"><span data-stu-id="c39c7-142">**Body** : `{}`</span></span>

<span data-ttu-id="c39c7-143">选择“ **导入** ”。</span><span class="sxs-lookup"><span data-stu-id="c39c7-143">Select **Import**.</span></span>

![连接器配置中的 "从示例导入" 对话框的屏幕截图](./images/import-sample.png)

<span data-ttu-id="c39c7-145">选择右上方的 " **创建连接器** "。</span><span class="sxs-lookup"><span data-stu-id="c39c7-145">Choose **Create Connector** on the top-right.</span></span> <span data-ttu-id="c39c7-146">创建连接器后，从 " **安全** " 页复制生成的 **重定向 URL** 。</span><span class="sxs-lookup"><span data-stu-id="c39c7-146">After the connector has been created, copy the generated **Redirect URL** from **Security** page.</span></span>

![生成的重定向 URL 的屏幕截图](./images/redirect-url.png)

<span data-ttu-id="c39c7-148">返回到在上一练习中创建的 [Azure 门户](https://aad.portal.azure.com) 中已注册的应用程序。</span><span class="sxs-lookup"><span data-stu-id="c39c7-148">Go back to the registered application in the [Azure Portal](https://aad.portal.azure.com) you created in the previous exercise.</span></span> <span data-ttu-id="c39c7-149">在左侧菜单上选择 " **身份验证** "。</span><span class="sxs-lookup"><span data-stu-id="c39c7-149">Select **Authentication** on the left-hand side menu.</span></span> <span data-ttu-id="c39c7-150">选择 " **添加平台** "，然后选择 " **Web** "。</span><span class="sxs-lookup"><span data-stu-id="c39c7-150">Select **Add a platform** , then select **Web**.</span></span> <span data-ttu-id="c39c7-151">输入 **重定向 uri** 中的上一步骤复制的重定向 URL，然后选择 " **配置** "。</span><span class="sxs-lookup"><span data-stu-id="c39c7-151">Enter the redirect URL copied from the previous step in the **Redirect URIs** , then select **Configure**.</span></span>

![Azure 门户中答复 Url 刀片的屏幕截图](./images/update-app-reg.png)

## <a name="option-2-create-custom-connector-by-importing-openapi-file"></a><span data-ttu-id="c39c7-153">选项2：通过导入 OpenAPI 文件创建自定义连接器</span><span class="sxs-lookup"><span data-stu-id="c39c7-153">Option 2: Create custom connector by importing OpenAPI file</span></span>

<span data-ttu-id="c39c7-154">使用文本编辑器，创建一个名为的新的空文件 `MSGraph-Delegate-Batch.swagger.json` ，并添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="c39c7-154">Using a text editor, create a new empty file named `MSGraph-Delegate-Batch.swagger.json` and add the following code.</span></span>

[!code-json[](../LabFiles/MSGraph-Delegate-Batch.swagger.json)]

<span data-ttu-id="c39c7-155">打开浏览器并导航到 " [Microsoft Power 自动](https://flow.microsoft.com)"。</span><span class="sxs-lookup"><span data-stu-id="c39c7-155">Open a browser and navigate to [Microsoft Power Automate](https://flow.microsoft.com).</span></span> <span data-ttu-id="c39c7-156">使用 Office 365 租户管理员帐户登录。</span><span class="sxs-lookup"><span data-stu-id="c39c7-156">Sign in with your Office 365 tenant administrator account.</span></span> <span data-ttu-id="c39c7-157">选择左侧菜单中的 " **数据** "，然后在下拉菜单中选择 " **自定义连接器** " 项。</span><span class="sxs-lookup"><span data-stu-id="c39c7-157">Choose **Data** on the left-hand side menu, and select the **Custom Connectors** item in the drop-down menu.</span></span>

<span data-ttu-id="c39c7-158">在 " **自定义连接器** " 页上，选择右上方的 **新自定义连接线** 链接，然后在下拉菜单中选择 " **导入 OpenAPI 文件** " 项。</span><span class="sxs-lookup"><span data-stu-id="c39c7-158">On the **Custom Connectors** page choose the **New custom connector** link in the top right, then select the **Import an OpenAPI file** item in the drop-down menu.</span></span>

<span data-ttu-id="c39c7-159">`MS Graph Batch Connector`在 " **连接器名称** " 文本框中输入。</span><span class="sxs-lookup"><span data-stu-id="c39c7-159">Enter `MS Graph Batch Connector` in the **Connector name** text box.</span></span> <span data-ttu-id="c39c7-160">选择要上传 OpenAPI 文件的文件夹图标。</span><span class="sxs-lookup"><span data-stu-id="c39c7-160">Choose the folder icon to upload the OpenAPI file.</span></span> <span data-ttu-id="c39c7-161">浏览到 `MSGraph-Delegate-Batch.swagger.json` 您创建的文件。</span><span class="sxs-lookup"><span data-stu-id="c39c7-161">Browse to the `MSGraph-Delegate-Batch.swagger.json` file you created.</span></span> <span data-ttu-id="c39c7-162">选择 " **继续** " 上传 OpenAPI 文件。</span><span class="sxs-lookup"><span data-stu-id="c39c7-162">Choose **Continue** to upload the OpenAPI file.</span></span>

<span data-ttu-id="c39c7-163">在 "连接器配置" 页上，选择 "导航" 菜单中的 " **安全** " 链接。</span><span class="sxs-lookup"><span data-stu-id="c39c7-163">On the connector configuration page, choose the **Security** link in the navigation menu.</span></span> <span data-ttu-id="c39c7-164">按如下所示填写字段。</span><span class="sxs-lookup"><span data-stu-id="c39c7-164">Fill in the fields as follows.</span></span>

- <span data-ttu-id="c39c7-165">**选择您的 API 实现的身份验证** ： `OAuth 2.0`</span><span class="sxs-lookup"><span data-stu-id="c39c7-165">**Choose what authentication is implemented by your API** : `OAuth 2.0`</span></span>
- <span data-ttu-id="c39c7-166">**标识提供程序** ： `Azure Active Directory`</span><span class="sxs-lookup"><span data-stu-id="c39c7-166">**Identity Provider** : `Azure Active Directory`</span></span>
- <span data-ttu-id="c39c7-167">**客户端 id** ：在上一练习中创建的应用程序 id</span><span class="sxs-lookup"><span data-stu-id="c39c7-167">**Client id** : the application ID you created in the previous exercise</span></span>
- <span data-ttu-id="c39c7-168">**客户端密码** ：在上一练习中创建的密钥</span><span class="sxs-lookup"><span data-stu-id="c39c7-168">**Client secret** : the key you created in the previous exercise</span></span>
- <span data-ttu-id="c39c7-169">**登录 url** ： `https://login.windows.net`</span><span class="sxs-lookup"><span data-stu-id="c39c7-169">**Login url** : `https://login.windows.net`</span></span>
- <span data-ttu-id="c39c7-170">**租户 ID** ： `common`</span><span class="sxs-lookup"><span data-stu-id="c39c7-170">**Tenant ID** : `common`</span></span>
- <span data-ttu-id="c39c7-171">**资源 URL** ： `https://graph.microsoft.com` (不带后缀/) </span><span class="sxs-lookup"><span data-stu-id="c39c7-171">**Resource URL** : `https://graph.microsoft.com` (no trailing /)</span></span>
- <span data-ttu-id="c39c7-172">**范围** ：保留为空</span><span class="sxs-lookup"><span data-stu-id="c39c7-172">**Scope** : Leave blank</span></span>

<span data-ttu-id="c39c7-173">选择右上方的 " **创建连接器** "。</span><span class="sxs-lookup"><span data-stu-id="c39c7-173">Choose **Create Connector** on the top-right.</span></span> <span data-ttu-id="c39c7-174">创建连接器后，复制生成的 **重定向 URL** 。</span><span class="sxs-lookup"><span data-stu-id="c39c7-174">After the connector has been created, copy the generated **Redirect URL**.</span></span>

![生成的重定向 URL 的屏幕截图](./images/redirect-url.png)

<span data-ttu-id="c39c7-176">返回到在上一练习中创建的 [Azure 门户](https://aad.portal.azure.com) 中已注册的应用程序。</span><span class="sxs-lookup"><span data-stu-id="c39c7-176">Go back to the registered application in the [Azure Portal](https://aad.portal.azure.com) you created in the previous exercise.</span></span> <span data-ttu-id="c39c7-177">在左侧菜单上选择 " **身份验证** "。</span><span class="sxs-lookup"><span data-stu-id="c39c7-177">Select **Authentication** on the left-hand side menu.</span></span> <span data-ttu-id="c39c7-178">选择 " **添加平台** "，然后选择 " **Web** "。</span><span class="sxs-lookup"><span data-stu-id="c39c7-178">Select **Add a platform** , then select **Web**.</span></span> <span data-ttu-id="c39c7-179">输入 **重定向 uri** 中的上一步骤复制的重定向 URL，然后选择 " **配置** "。</span><span class="sxs-lookup"><span data-stu-id="c39c7-179">Enter the redirect URL copied from the previous step in the **Redirect URIs** , then select **Configure**.</span></span>

![Azure 门户中答复 Url 刀片的屏幕截图](./images/update-app-reg.png)

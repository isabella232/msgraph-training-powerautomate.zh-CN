---
ms.openlocfilehash: bf83723de025f3e1f6bde5b4226fc8966dff6b9a
ms.sourcegitcommit: 64947f11d367ffbebbafb700fdfdc20617275f35
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "48829632"
---
<!-- markdownlint-disable MD002 MD041 -->

确保连接器可供使用的最后一个配置步骤是授权和测试自定义连接器以创建缓存的连接。

> [!IMPORTANT]
> 以下步骤要求您使用管理员权限登录。

在 [Microsoft 电力自动化](https://flow.microsoft.com)中，转到左侧的 " **数据** " 菜单项，然后选择 " **连接** " 页。 选择 " **新建连接** " 链接。

!["新建连接" 按钮的屏幕截图](./images/new-connection.png)

通过单击加号按钮找到您的自定义连接器并完成连接。 使用 Office 365 租户管理员的 Azure Active Directory 帐户登录。

!["连接" 列表的屏幕截图](./images/connection-sign-in.png)

当系统提示您输入请求的权限时，请选中 " **代表您的组织同意"** ，然后选择 " **接受** " 以授权权限。

![同意提示的屏幕截图](./images/consent-prompt.png)

授权权限后，会在 "自动使用电源" 中创建连接。

现在已配置并启用自定义连接器。 可能在应用权限中存在延迟且可用，但现在已配置连接器。

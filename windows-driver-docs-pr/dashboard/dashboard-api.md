---
title: 硬件仪表板 API
description: “Microsoft 硬件 API”以编程方式在组织的合作伙伴中心帐户中查询和创建硬件产品提交。
ms.topic: article
ms.date: 09/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7cec191850f774186b0c564eecd36137881217e7
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "75209249"
---
# <a name="hardware-dashboard-api"></a>硬件仪表板 API

使用“Microsoft 硬件 API”  以编程方式在组织的合作伙伴中心帐户中查询和创建硬件产品提交。 如果你的帐户管理多个产品，并且你想要自动执行并优化这些资源的提交过程，那么这些 API 非常有用。 这些 API 使用 Azure Active Directory (Azure AD) 验证来自应用或服务的调用。
以下步骤介绍了使用“Microsoft 硬件 API”的端到端过程：

1. 这些 API 仅可供属于硬件[合作伙伴中心计划](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-started-with-the-hardware-dashboard)的帐户使用。

2. 确保已完成以下先决条件。

3. 在“Microsoft 硬件 API”中调用某个方法之前，请先获取 Azure AD 访问令牌，如下所示。 获取令牌后，可以在 60 分钟的令牌有效期内，使用该令牌调用“Microsoft Store 提交 API”。 该令牌到期后，可以重新生成一个。

4. 调用“Microsoft 硬件 API”。

## <a name="complete-the-prerequisites-for-using-the-microsoft-hardware-api"></a>完成使用“Microsoft 硬件 API”的先决条件

在开始编写调用“Microsoft 硬件 API”的代码之前，确保已满足以下必需的先决条件。

* 你（或你的组织）必须具有 Azure AD 目录，并且你必须具有该目录的[全局管理员](https://go.microsoft.com/fwlink/?LinkId=746654)权限。 如果你已使用 Office 365 或 Microsoft 的其他业务服务，表示你已经具有 Azure AD 目录。 否则，你可以免费[在合作伙伴中心中创建新的 Azure AD](https://docs.microsoft.com/windows/uwp/publish/associate-azure-ad-with-partner-center#create-a-brand-new-azure-ad-to-associate-with-your-partner-center-account)。

* 如果 Azure AD 应用程序不存在，则[必须创建一个](https://docs.microsoft.com/windows/uwp/publish/add-users-groups-and-azure-ad-applications#create-a-new-azure-ad-application-account-in-your-organizations-directory-and-add-it-to-your-partner-center-account)。

* 必须[将 Azure AD 应用程序与你的合作伙伴中心帐户相关联](https://docs.microsoft.com/windows/uwp/publish/associate-azure-ad-with-partner-center)，并为该帐户分配“管理员”角色。 

* 收集 [Azure AD 应用程序租户 ID、客户端 ID 和密钥](https://docs.microsoft.com/windows/uwp/publish/add-users-groups-and-azure-ad-applications#manage-keys-for-an-azure-ad-application)。  **请务必打印或复制此密钥信息，因为在离开密钥创建页面后，你将无法再访问该信息。** 

## <a name="assigning-the-appropriate-hardware-roles-to-your-azure-ad-application"></a>将适当的硬件角色分配给 Azure AD 应用程序

当你满足以上先决条件以后，我们现在必须分配适当的角色，让 Azure AD 应用程序可以创建并管理提交内容和发货标签。

1. 请从合作伙伴中心选择齿轮图标（靠近仪表板右上角），然后选择“开发人员设置”  。 在“设置”菜单中，选择“用户”。  

2. 在“用户”页面上，选择“Azure AD 应用程序”，然后选择特定的 Azure AD 应用程序，即用于访问合作伙伴中心帐户的已提交内容的应用或服务。    

3. 在此页面上，在“角色”  下，单击“硬件”  。

    ![一个显示了“角色”部分中的“硬件”选项卡的图像](images/hardware-tab-in-roles-section.png)

    选择“驱动程序提交者”  、“发货标签所有者”  ，以及“发货标签推广者”（如果可用）。   [详细了解这些角色](https://docs.microsoft.com/windows-hardware/drivers/dashboard/managing-user-roles)
    

## <a name="obtain-an-azure-ad-access-token"></a>获取 Azure AD 访问令牌

在“Microsoft 硬件 API”中调用任何方法之前，首先必须获取将传递给该 API 中每个方法的 **Authorization** 标头的 Azure AD 访问令牌。 获取访问令牌后，在它到期前，你有 60 分钟的使用时间。 该令牌到期后，可以对它进行刷新，以便可以在之后调用该 API 时继续使用。 若要获取访问令牌，请按照 [使用客户端凭据的服务到服务调用](https://azure.microsoft.com/documentation/articles/active-directory-protocols-oauth-service-to-service/) 中的说明将 HTTP POST 发送到 `https://login.microsoftonline.com/<tenant_id>/oauth2/token` 终结点。 示例请求如下所示。

```cpp
POST https://login.microsoftonline.com/<tenant_id>/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8

grant_type=client_credentials
&client_id=<your_client_id>
&client_secret=<your_client_secret>
&resource=https://manage.devcenter.microsoft.com
```

对于 POST URI 中的 *tenant_id* 值以及 *client_id* 和 *client_secret* 参数，请指定在上一部分中从合作伙伴中心中为应用程序检索的租户 ID、客户端 ID 和密钥。 对于 *resource* 参数，必须指定 `https://manage.devcenter.microsoft.com`。

在你的访问令牌到期后，你可按照[刷新访问令牌](https://azure.microsoft.com/documentation/articles/active-directory-protocols-oauth-code/#refreshing-the-access-tokens)中的说明刷新令牌。

## <a name="use-the-microsoft-hardware-api"></a>使用“Microsoft 硬件 API”

获取 Azure AD 访问令牌后，可以在“Microsoft 硬件 API”中调用方法。 该 API 包括许多分组到各个方案中的方法。 若要创建或更新提交，一般需在“Microsoft 硬件 API”中按特定顺序调用多个方法。 有关每个方案和每个方法的语法的信息，请参阅下表中的文章。

| 方案 | 说明 |
|:--|:--|
| 驱动程序 | 获取、创建和更新向你的合作伙伴中心帐户注册的驱动程序。 有关这些方法的详细信息，请参阅以下文章：<ul><li>[获取产品数据](get-product-data.md)</li><li>[管理产品提交](manage-product-submissions.md)</li><li>[获取发货标签数据](get-shipping-labels.md)</li><li>[管理发货标签](manage-shipping-labels.md)</li></ul>|

## <a name="code-examples"></a>代码示例

以下示例提供了详细的代码，演示如何结合 Microsoft Surface 和设备团队创建的完整端到端预生成解决方案使用 Microsoft 硬件 API：

* [C# 示例](https://download.microsoft.com/download/C/F/4/CF404E53-87A0-4204-BA13-A64B09A237C1/HardwareApiCSharpSample.zip)

[硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)

[Surface 开发人员中心管理器工具 (GitHub)](https://github.com/Microsoft/SDCM)

## <a name="additional-help"></a>其他帮助

如果你对“Microsoft Store 提交 API”有疑问，或需要获取有关使用此 API 来管理提交的帮助，请访问[支持页面](https://partner.microsoft.com/dashboard/account/help?returnUri=https://developer.microsoft.com/dashboard/hardware)并请求帮助。

## <a name="related-topics"></a>相关主题

[什么是 Azure Active Directory？](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis)

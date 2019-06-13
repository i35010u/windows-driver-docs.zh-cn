---
title: 启用安全数据共享
description: 使用硬件仪表板 API 以安全方式下载驱动程序提交失败数据所需的步骤。
ms.author: shganesh
ms.topic: article
ms.date: 09/28/2018
ms.localizationpriority: medium
ms.openlocfilehash: 37aadceb87ad2d3aaf183ce23efe848590df1894
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63335108"
---
# <a name="enable-secure-data-sharing"></a>启用安全数据共享

为了使用 API 以安全方式下载驱动程序提交失败数据，你必须将以下有关用于访问报告 API 的 Azure AD 应用的信息发送到 Microsoft Store Partner Operations ([partnerops@microsoft.com](mailto:partnerops@microsoft.com))。

|Azure AD 应用信息|格式|
|----|----|
|ApplicationId|*\<YourAppGuid>*|
|DisplayName|*\<YourAppName>*|
|主页 URL|*\<URL>*|
|应用程序类型|**Web 应用**（假设是 Web 应用）|
|多租户|**是**（如果这不是多租户，你可以使其为多租户）|

* 请确保该应用具有以下权限：

  * Windows AAD - **登录**和**读取用户配置文件**

  * Azure 存储 - **访问 Azure 存储**

可以在 Azure AD 应用的“仪表板”视图、“已注册应用”窗格、“属性”窗格以及“所需权限”和“启用访问权限”窗格中找到此信息。 以下屏幕截图显示了找到数据的位置。

![“已注册应用”、“设置”和“属性”窗格的屏幕截图](./images/app-settings.png)

![“所需权限”和“启用访问权限”窗格的屏幕截图](./images/permissions-access.png)

如需安全数据共享问题的帮助和解答，请通过 [partnerops@microsoft.com](mailto:partnerops@microsoft.com) 向 Microsoft Store Partner Operations 发送邮件。

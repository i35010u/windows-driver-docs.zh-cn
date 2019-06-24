---
title: 注册硬件计划
description: 注册硬件计划
ms.assetid: 8E947636-7F0E-4C31-9149-D6BF60D84226
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8236e67db1829e08b493197ccce4c5fed0265463
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "65106395"
---
# <a name="register-for-the-hardware-program"></a>注册硬件计划

组织管理员必须[注册](https://go.microsoft.com/fwlink/?LinkID=828002) Windows 硬件开发人员中心计划。

> [!Note]
> 如果在此过程中需要支持，请开具支持票证： https://developer.microsoft.com/windows/support 。  
>- 依次选择“联系我们”  、“仪表板问题”  ，然后从下拉列表中选择“硬件提交和签名(所有 OS 版本)”  。  
>- 实时聊天和电子邮件支持时间为星期一至星期五上午 8 点到晚上 8 点（中部标准时间）。  电子邮件支持的初始响应 SLA 为 24-48 小时。

## <a name="before-you-sign-up"></a>注册之前

在开始注册过程前查看以下要求。

- 如果有要用于硬件计划的现有组织开发人员中心帐户，请在开始注册前使用该帐户登录。

- 必须具有扩展验证 (EV) 代码签名证书。 检查你的组织是否已有代码签名证书。 如果组织已有证书，由于系统将要求你为文件签名，请提供该证书。 如果组织没有证书，将需要在注册过程中购买证书。

    有关代码签名证书和如何获取证书的信息，请参阅[获取代码签名证书](get-a-code-signing-certificate.md)。

- 你将需要使用组织的 Azure Active Directory (Azure AD) [全局管理员](https://go.microsoft.com/fwlink/?LinkId=746654)帐户登录。 如果不知道组织是否有 Azure AD 目录，请联系 IT 部门。 如果组织没有 Azure AD 目录，必须能创建一个。

- 必须有权代表组织签署法律协议。

## <a name="registration-steps"></a>注册步骤

硬件计划注册有五个主要步骤。

1. 获取代码签名证书

    - 确保具有代码签名证书

    - 如果没有证书，必须购买证书并提供该证书。

2. 下载 signtool.exe
    - signtool.exe 作为 [Windows SDK 下载](https://developer.microsoft.com/windows/downloads/windows-10-sdk)的一部分提供

3. 在注册过程的“签名并上传”  部分中为提供给你的文件签名并上传。
    > [!NOTE]
    > 不再需要在同一浏览器会话中完成以下三个步骤。

    1. 下载提供的可签名文件。
    2. 使用 signtool.exe 和代码签名证书为文件签名。
    3. 上传已签名的文件。 从已签名文件中提取组织名称和 ID 编号。

4. 使用 Azure AD 全局管理员帐户登录

    - 如果组织已有 Azure AD 目录，请使用[全局管理员](https://go.microsoft.com/fwlink/?LinkId=746654)帐户登录。

    - 如果组织没有 Azure AD 目录，必须创建一个目录并登录。

5. 帐户详细信息

    - 输入帐户详细信息，如组织显示名称和个人联系信息。

    - 为所需的硬件开发人员法律协议签名，该协议位于帐户设置选项卡上，如下所示：

        ![显示“协议”按钮的图像。](images/legal-agreements-location.png)

## <a name="after-registration"></a>注册之后

注册完成后，提供其他管理任务：

- [管理用户和权限](managing-user-roles.md)

完成任何管理任务后，你随时可以创建首个硬件提交。 有关信息和说明，请参阅[硬件提交](hardware-certification-submissions.md)。

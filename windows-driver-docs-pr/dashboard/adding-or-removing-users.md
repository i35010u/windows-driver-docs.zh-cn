---
title: 添加或删除用户
description: 硬件仪表板将 Azure Active Directory 用于用户管理。 此主题介绍使用全局管理员凭据添加/删除用户的过程。
ms.assetid: 1922C767-CD34-43CD-AF90-F1FCA297EF5E
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb5dcefa805a8577e7fcbf2a008ef500d218296d
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63337333"
---
# <a name="adding-or-removing-users"></a>添加或删除用户

合作伙伴中心使用 Azure Active Directory 进行用户管理。 这意味着你需要使用开发人员门户全局管理员帐户凭据来添加或删除用户。 如果已丢失或不确定是否具有全局管理员凭据，请联系支持人员。 请注意，开发人员门户全局管理员帐户凭据与 Azure AD 全局管理员帐户凭据不同。

全局管理员是用于注册硬件计划的帐户。 如果你的帐户已从 Sysdev 中迁移，则已通过电子邮件通知了你的全局管理员。 如果已丢失或不确定是否具有全局管理员凭据，请联系支持人员。

若要开始使用，请导航到 [帐户设置](https://go.microsoft.com/fwlink/?linkid=833506)页面，然后以全局管理员身份登录。选择左侧的“管理用户”  。

## <a name="adding-users"></a>添加用户

若要添加用户，请选择“添加用户”  。

![显示合作伙伴中心的“管理用户”菜单的图像](images/manage-users.png)

这将加载与你的 Azure Active Directory 租户关联的所有用户。 可以通过选中相应用户名称旁边的复选框，将现有用户添加到合作伙伴中心。 若要将新用户与你的租户相关联，请选择“新用户”  。

![显示合作伙伴中心的“添加用户”菜单的图像](images/add-users.png)

在“新用户”  屏幕上，提供新用户的详细信息。 需要新用户的名字和姓氏，以及他们将用于登录的自定义用户名。 还可以将他们添加到你已在你的目录中创建的任何组。 最后，可以授予他们为实现硬件计划所需的任何角色。

![显示“新建用户”屏幕以及注册新用户所需的详细信息的图像](images/new-user-screen.png)

当所有详细信息完成填写后，请选择“保存”  以完成新用户信息填写。 这会将授予所选权限的用户添加到你的帐户，并为他们生成一次性使用的密码。

**注意**  确保为新用户打印或保存此页面。 离开此页面后，将无法恢复该密码。

## <a name="removing-users"></a>删除用户

删除用户非常方便。 在“管理用户”  页上，会看到当前有权访问你的合作伙伴中心帐户的所有用户列表。 若要删除其中一个用户，只需选择最右侧的“删除”  。

![显示“管理用户”屏幕上的“删除”按钮的图像](images/remove-users.png)

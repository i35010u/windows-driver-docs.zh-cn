---
title: AllSigningEqual 组策略
description: AllSigningEqual 组策略
ms.assetid: b23eed87-76ce-4447-86d2-2be370ee57c5
keywords:
- 驱动程序选择 WDK 设备安装，AllSigningEqual 组策略
- 查找设备安装 WDK 设备安装的驱动程序，AllSigningEqual 组策略
- 在设备安装 WDK 设备安装过程中搜索驱动程序，AllSigningEqual 组策略
- AllSigningEq
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6a9690da38be7bf4db85917eb768f6fea2d5431
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096249"
---
# <a name="allsigningequal-group-policy"></a>AllSigningEqual 组策略


如果禁用了 **AllSigningEqual** 组策略，windows 签名颁发机构签署的 windows 将对 windows 签名颁发机构签名的驱动程序 (Microsoft 签名) 比具有以下功能之一的驱动程序更好：

-   [Authenticode](authenticode.md)签名。

-   低于驱动程序的[设备安装程序类](./overview-of-device-setup-classes.md)的[LowerLogoVersion](lowerlogoversion.md)值的 Windows 版本的 Microsoft 签名。

如果 **AllSigningEqual** 组策略处于禁用状态，则 windows 将选择由 windows 签名颁发机构通过 authenticode 签名的驱动程序签名的驱动程序，即使 authenticode 签名的驱动程序更适合设备也是如此。

来自 Windows 签名颁发机构的签名平等排名，并包括以下签名类型：

-   高级 WHQL 签名和标准 WHQL 签名

-   收件箱驱动程序的签名

-   Windows 持续工程 (SE) 签名

-   Windows 版本的 WHQL 签名，该签名与驱动程序的[设备安装程序类](./overview-of-device-setup-classes.md)的[LowerLogoVersion](lowerlogoversion.md)值相同或更高。

网络管理员可以通过启用 **AllSigningEqual** 组策略来更改此行为。 这会将 Windows 配置为在选择与设备最匹配的驱动程序时，将所有 Microsoft 签名类型和 Authenticode 签名视为相等，并按级别进行排序。

**注意**   从 Windows 7 开始，默认情况下启用**AllSigningEqual**组策略。

 

例如，假设网络管理员必须在网络上配置客户端计算机以安装驱动程序，如下所示：

-   仅当驱动程序具有由企业证书颁发机构颁发的验证码签名（ (CA) 为网络创建）时，客户端计算机才应安装新驱动程序。 企业可能要执行此操作，以确保在客户端计算机上安装的所有驱动程序均已签名，并且除 Microsoft 以外的唯一受信任签名颁发机构是企业管理的 CA。

-   对于签名的驱动程序，不应使用签名评分来确定具有最佳等级的驱动程序。 仅使用功能分数和标识符分数的总和来比较驱动因素排名。 例如，如果新驱动程序的功能分数和标识符分数的总和低于收件箱驱动程序的对应总和，则 Windows 将安装新驱动程序。

为实现此目的，网络管理员：

-   将企业 CA 证书添加到客户端计算机的受信任的发布者存储区。

-   启用客户端计算机上的 **AllSigningEqual** 组策略。

网络管理员以这种方式配置客户端计算机后，管理员可以签署具有企业 CA 证书的驱动程序，并将驱动程序分发到客户端计算机。 在此配置中，如果功能分数与标识符分数之和低于 Microsoft 签名驱动程序的对应总和，则客户端计算机上的 Windows 将为设备而不是 Microsoft 签名驱动程序安装新的驱动程序。

按照以下步骤配置 Windows Vista 和更高版本的 Windows 上的 AllSigningEqual 组策略：

1.  在 "开始" 菜单上，单击 " **运行"。**

2.  输入 **gpedit.msc** 以执行组策略编辑器，然后单击 **"确定"**。

3.  在组策略编辑器的左窗格中，单击 " **计算机配置**"。

4.  在 " **管理模板** " 页上，双击 " **系统**"。

5.  在 " **系统** " 页上，双击 " **设备安装**"。

6.  选择 **"在驱动程序排名和选择过程中平均处理所有数字签名的驱动程序"** ，然后单击 " **属性**"。

7.  在 " **设置** " 选项卡上，选择 " **已启用** " (启用 **AllSigningEqual** 组策略) 或 **禁用** (，以禁用 **AllSigningEqual** 组策略) 。

若要确保在目标系统上更新设置，请执行以下操作：

1.  创建 *Cmd.exe*的桌面快捷方式，右键单击 *Cmd.exe* 快捷方式，然后选择 "以 **管理员身份运行**"。

2.  在命令提示符窗口中，运行组策略更新实用工具， *GPUpdate.exe*。

此配置更改将进行一次，并适用于计算机上的所有后续驱动程序安装，直到重新配置 AllSigningEqual。

有关驱动程序排名的详细信息，请参阅 [Windows 如何对驱动程序](how-setup-ranks-drivers--windows-vista-and-later-.md)进行排名。

 


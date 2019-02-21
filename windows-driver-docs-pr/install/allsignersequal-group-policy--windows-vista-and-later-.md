---
title: AllSignersEqual 组策略
description: AllSignersEqual 组策略
ms.assetid: b23eed87-76ce-4447-86d2-2be370ee57c5
keywords:
- 驱动程序选择 WDK 设备安装，AllSignersEqual 组策略
- 查找设备安装 WDK 设备安装，AllSignersEqual 组策略的驱动程序
- 设备安装 WDK 设备安装期间，AllSignersEqual 组策略搜索驱动程序
- AllSignersEq
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 041b54848394db70e3c2f4159118251167f78518
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546779"
---
# <a name="allsignersequal-group-policy"></a>AllSignersEqual 组策略


如果**AllSignersEqual**禁用组策略，Windows 驱动程序签名的签名颁发机构 （Microsoft 签名） 好于驱动程序具有以下项之一的 Windows 级别：

-   [Authenticode](authenticode.md)签名。

-   Windows 版本的 Microsoft 签名早于[LowerLogoVersion](lowerlogoversion.md)驱动程序的值[设备安装程序类](device-setup-classes.md)。

如果**AllSignersEqual**组策略禁用，则 Windows 选择由签名颁发机构验证码签名的驱动程序，通过 Windows 签名，即使该验证码签名的驱动程序在其他方面更好的匹配到设备的驱动程序。

从 Windows 签名颁发机构签名同样排名，并包括以下签名类型：

-   高级 WHQL 签名和标准 WHQL 签名

-   收件箱驱动程序签名

-   Windows 可持续工程 (SE) 签名

-   相同的 Windows 版本的 WHQL 签名或晚于[LowerLogoVersion](lowerlogoversion.md)驱动程序的值[设备安装程序类](device-setup-classes.md)。

网络管理员可以更改此行为，从而**AllSignersEqual**组策略。 这会配置 Windows 以选择最匹配到设备的驱动程序时将所有 Microsoft 签名类型和验证码签名都将视为相对于排名等于。

**请注意**  从 Windows 7 开始**AllSignersEqual**默认情况下启用组策略。

 

例如，考虑这种情况，则网络管理员必须配置客户端计算机上安装的驱动程序，如下所示的网络：

-   仅当该驱动程序具有验证码签名颁发为网络中创建企业证书颁发机构 (CA) 由客户端计算机应安装新的驱动程序。 企业可能想要执行此操作以确保客户端计算机安装的所有驱动程序进行签名，并且仅受信任签名颁发机构不是 Microsoft 为企业管理的 CA。

-   有关签名的驱动程序，签名分数应不用于确定具有最佳的排名的驱动程序。 仅特征评分和标识符得分的总和用于比较驱动程序的排名。 例如，如果总和的特征评分和新的驱动程序的标识符分数低于收件箱驱动程序的相应之和，Windows 将安装新的驱动程序。

为此，网络管理员：

-   将企业 CA 证书添加到客户端计算机的受信任发布者存储。

-   使**AllSignersEqual**客户端计算机上的组策略。

网络管理员以这种方式配置客户端计算机后，管理员可以签名的驱动程序具有企业 CA 证书和分发到客户端计算机的驱动程序。 在此配置中，客户端计算机上的 Windows 将安装而不是 Microsoft 签名的驱动程序设备的新驱动程序，如果功能得分和标识符得分的总和低于 Microsoft 签名的驱动程序的相应之和。

请按照以下步骤来配置 AllSignersEqual 组策略在 Windows Vista 和更高版本的 Windows 上操作：

1.  在开始菜单上单击**运行。**

2.  输入**GPEdit.msc**来执行组策略编辑器，然后单击**确定**。

3.  在组策略编辑器的左窗格中，单击**计算机配置**。

4.  上**管理模板**页上，双击**系统**。

5.  上**系统**页上，双击**设备安装**。

6.  选择**驱动程序分级和选择过程中同样对待所有经过数字签名的驱动程序**，然后单击**属性**。

7.  上**设置**选项卡上，选择**已启用**(若要启用**AllSignersEqual**组策略) 或**禁用**(若要禁用**AllSignersEqual**组策略)。

若要确保在目标系统上更新的设置，请执行以下操作：

1.  创建桌面快捷方式*Cmd.exe*，右键单击*Cmd.exe*快捷方式，然后选择**以管理员身份运行**。

2.  从命令提示符窗口中，运行组策略更新实用工具*GPUpdate.exe*。

此配置更改进行一次，直到 AllSignersEqual 重新配置适用于所有后续的驱动程序安装在计算机上。

有关驱动程序分级的详细信息，请参阅[如何 Windows Ranks Drivers](how-setup-ranks-drivers.md)。

 

 






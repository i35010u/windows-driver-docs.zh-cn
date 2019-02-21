---
title: 概述安装专用生成的收件箱驱动程序
description: 概述安装专用生成的收件箱驱动程序
ms.assetid: eec9474c-5aad-4b81-b7df-5e89cbfe92ab
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81b932c128bc20b87c13ad617e99ef47ea6ebbf6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546060"
---
# <a name="overview-of-installing-private-builds-of-inbox-drivers"></a>概述安装专用生成的收件箱驱动程序


从开始 Windows Vista 的计算机系统上安装插即用 (PnP) 设备时，Windows 选择驱动程序基于几个因素，例如[硬件 ID](hardware-ids.md)或[兼容 ID](compatible-ids.md)，日期，和版本。 Windows 分析这些因素分配指示驱动程序与设备的匹配程度的排名。 越低排名，更好的匹配驱动程序是用于设备。

此外，Windows vista 中，从开始，如果驱动程序包含来自 Windows 签名颁发机构 （Microsoft 签名） 的签名，Windows 进行排名其优于另一个驱动程序签名时使用的同一个设备：

-   第三方发布的签名。 使用生成此类型的签名[软件发布者证书](software-publisher-certificate.md)从 Microsoft 授权颁发证书，此类第三方证书颁发机构 (CA) 获取。

-   早于的 Windows 版本的 Microsoft 签名[LowerLogoVersion](lowerlogoversion.md)驱动程序的值[设备安装程序类](device-setup-classes.md)。

Microsoft 签名类型包括：

-   高级 WHQL 签名和标准 WHQL 签名

-   收件箱驱动程序签名

-   Windows 可持续工程 (Windows SE) 签名

-   相同的 Windows 版本的 WHQL 签名或更高版本比指定的 Windows 版本[LowerLogoVersion](lowerlogoversion.md)为驱动程序的设备安装程序类设置的值

**请注意**  Windows 即使具有第三方签名的驱动程序是设备的更好地匹配项，选择具有 Microsoft 签名的驱动程序。 使用发布服务器标识证书\[PIC\]的第三方签名不会更改此行为。

 

从 Windows Vista 开始[ **AllSignersEqual**组策略](allsignersequal-group-policy--windows-vista-and-later-.md)控制 Windows 进行 Microsoft 签名的驱动程序和第三方签名的驱动程序的排名。 当**AllSignersEqual**是启用，Windows 将所有 Microsoft 签名和第三方签名视为等方面排名时选择的驱动程序是设备的最佳匹配项。

**请注意**  在 Windows Vista 和 Windows Server 2008 **AllSignersEqual**组策略在默认情况下处于禁用状态。 从 Windows 7 开始，默认情况下启用此组策略。

 

若要安装的收件箱驱动程序对专用生成，必须执行以下操作：

-   生成的收件箱驱动程序的专用版本。 您必须确保，专用生成优先于 Microsoft 签名版本时签名都被同等对待。 专用生成也必须进行数字签名通过使用提供的工具和 WDK 中。

    有关详细信息，请参阅[创建收件箱驱动程序对专用生成](creating-a-private-build-of-an-in-box-driver.md)。

-   启用[AllSignersEqual 组策略](allsignersequal-group-policy--windows-vista-and-later-.md)目标系统上，以便操作系统查看所有 Microsoft 签名类型和秩等于作为第三方签名选择驱动程序时，是设备的最佳匹配项。

    有关详细信息，请参阅[配置到同样上排名驱动程序签名的 Windows](configuring-windows-to-rank-driver-signatures-equally.md)。

有关 Windows 驱动程序的级别的详细信息，请参阅[Windows 中如何选择驱动程序](how-setup-selects-drivers.md)。

 

 






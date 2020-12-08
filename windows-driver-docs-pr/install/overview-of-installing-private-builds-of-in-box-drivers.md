---
title: 安装收件箱驱动程序的专用版本概述
description: 安装收件箱驱动程序的专用版本概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba38eac057a1ea4b8dcfb9f7014ef3282a192a87
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816681"
---
# <a name="overview-of-installing-private-builds-of-inbox-drivers"></a>安装收件箱驱动程序的专用版本概述


从 Windows Vista 开始，当计算机系统上安装了即插即用 (PnP) 设备时，Windows 会根据多种因素（如 [硬件 ID](hardware-ids.md) 或 [兼容 ID](compatible-ids.md)、日期和版本）选择驱动程序。 Windows 会分析这些因素，以便分配一个指示驱动程序与设备的匹配程度的级别。 排名越低，设备的驱动程序匹配就越好。

此外，从 Windows Vista 开始，如果驱动程序具有来自 Windows 签名颁发机构的签名 (Microsoft 签名) ，Windows 会将其排名好于使用签名的同一设备的另一个驱动程序：

-   第三方版本签名。 这种类型的签名是使用从第三方证书颁发机构获取的 [软件发行者证书](software-publisher-certificate.md) 生成的，该证书由 Microsoft 授权 () CA 颁发此类证书。

-   早于驱动程序的[设备安装程序类](./overview-of-device-setup-classes.md)的[LowerLogoVersion](lowerlogoversion.md)值的 Windows 版本的 Microsoft 签名。

Microsoft 签名类型包括以下内容：

-   高级 WHQL 签名和标准 WHQL 签名

-   收件箱驱动程序的签名

-   Windows (Windows SE) 签名的 windows 持续工程设计

-   Windows 版本的 WHQL 签名，该签名与为驱动程序的设备安装程序类设置的 [LowerLogoVersion](lowerlogoversion.md) 值指定的 windows 版本相同或更高

**注意**  即使具有第三方签名的驱动程序比设备更匹配，Windows 也会选择包含 Microsoft 签名的驱动程序。 使用 publisher 标识证书 \[ PIC \] 作为第三方签名不会更改此行为。

 

从 Windows Vista 开始， [ **AllSignersEqual** 组策略](./allsigningequal-group-policy.md)控制 Windows 如何排名 Microsoft 签署的驱动程序和第三方签名的驱动程序。 如果启用了 **AllSignersEqual** ，则在选择最匹配设备的驱动程序时，Windows 会将所有 Microsoft 签名和第三方签名视为相等，并按级别进行排序。

**注意**  在 Windows Vista 和 Windows Server 2008 中，默认情况下， **AllSignersEqual** 组策略处于禁用状态。 从 Windows 7 开始，默认情况下会启用此组策略。

 

若要安装收件箱驱动程序的专用版本，必须执行以下操作：

-   构建收件箱驱动程序的专用版。 当签名被同等对待时，必须确保专用生成先 Microsoft 签名版本。 还必须使用随 WDK 提供的工具对专用生成进行数字签名。

    有关详细信息，请参阅 [创建收件箱驱动程序的专用生成](creating-a-private-build-of-an-in-box-driver.md)。

-   启用目标系统上的 [AllSignersEqual 组策略](./allsigningequal-group-policy.md) ，以便在选择最匹配设备的驱动程序时，操作系统会查看所有 Microsoft 签名类型和第三方签名的排名是否相等。

    有关详细信息，请参阅 [将 Windows 配置为平等排列驱动程序签名](configuring-windows-to-rank-driver-signatures-equally.md)。

有关 Windows 如何对驱动程序进行排名的详细信息，请参阅 [Windows 如何选择驱动程序](./how-windows-selects-a-driver-for-a-device.md)。


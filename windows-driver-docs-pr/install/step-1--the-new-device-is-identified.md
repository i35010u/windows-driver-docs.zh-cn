---
title: 步骤1确定了新设备
description: 步骤1确定了新设备
ms.assetid: e0df70ca-cea3-44a1-b5ff-407f72a216f9
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: f0ab1d4c956403fb9fac8f2174594dd081f68e8d
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007638"
---
# <a name="step-1-the-new-device-is-identified"></a>第 1 步：标识新设备


在为新设备安装驱动程序之前，设备所连接到的总线或集线器驱动程序将为设备分配[硬件标识符（ID）](hardware-ids.md) 。 Windows 使用硬件 Id 查找设备与包含设备驱动程序的[驱动程序包](driver-packages.md)之间最近的匹配项。 有关硬件 Id 的详细信息，请参阅[设备标识字符串](device-identification-strings.md)。

硬件 ID 的格式通常由以下内容组成：

-   特定于总线的前缀，如 PCI @ no__t 或 USB @ no__t-1。
-   设备的供应商特定标识符，如供应商、型号和修订标识符。 硬件 ID 内的这些标识符的格式也特定于总线驱动程序。

独立硬件供应商（IHV）还可以为设备定义一个或多个[兼容的 id](compatible-ids.md) 。 兼容 Id 的格式与硬件 Id 相同;但是，它们通常比硬件 Id 更通用，不需要特定的制造商或型号信息。 如果操作系统无法找到设备硬件 ID 的匹配驱动程序包，则 Windows 将使用这些标识符为设备选择[驱动程序包](driver-packages.md)。 Ihv 为驱动程序包的[INF 文件](overview-of-inf-files.md)中的设备指定一个或多个兼容的 id。

Windows 使用硬件 Id 和兼容 Id 搜索设备的[驱动程序包](driver-packages.md)。 它通过将设备的硬件 Id 和兼容 Id 与包[INF 文件](overview-of-inf-files.md)中指定的 id 进行比较，找到设备的匹配驱动程序包。

例如，当用户将无线局域网（WLAN）适配器插入连接到计算机的 USB 集线器的端口时，将执行以下步骤：

1.  USB 集线器驱动程序检测到设备。 根据它从适配器查询的信息，集线器驱动程序会创建设备的硬件 ID。

    例如，USB 集线器驱动程序可以为 WLAN 适配器创建 USB @ no__t-0VID_1234 & PID_5678 & REV_0001 的硬件 ID，其中：

    -   VID_1234 是供应商的标识符。
    -   PID_5678 是设备的产品或型号，标识符。
    -   REV_0001 是设备的修订版本标识符。

    有关 USB 硬件 Id 格式的详细信息，请参阅[Usb 设备的标识符](identifiers-for-usb-devices.md)。

2.  USB 集线器驱动程序通知[即插即用（PnP）管理器](pnp-manager.md)检测到新设备。 PnP 管理器会查询集线器驱动程序的所有设备的硬件 Id。 集线器驱动程序可以为同一设备创建多个硬件 Id。

3.  [PnP 管理器](pnp-manager.md)通知 Windows 需要安装新的设备。 作为此通知的一部分，将向 Windows 提供硬件 Id 列表。

4.  Windows 将开始搜索与设备的某个硬件 Id 相匹配的[驱动程序包](driver-packages.md)。 如果 Windows 找不到匹配的硬件 ID，则会搜索具有与设备匹配的兼容 ID 的驱动程序包。

    有关此过程的详细信息，请参阅 [Step 2：已选中 @ no__t-0 的设备驱动程序。

每个总线驱动程序以其自己的特定于总线的方式构造硬件 Id。

有关其他总线的标准标识符的示例，请参阅：

*  [PCI 设备的标识符](identifiers-for-pci-devices.md)
*  [SCSI 设备的标识符](identifiers-for-scsi-devices.md)
*  [IDE 设备的标识符](identifiers-for-ide-devices.md)
*  [PCMCIA 设备的标识符](identifiers-for-pcmcia-devices.md)
*  [ISAPNP 设备的标识符](identifiers-for-isapnp-devices.md)
*  [1394设备的标识符](identifiers-for-1394-devices.md)
*  [安全数字（SD）设备的标识符](identifiers-for-secure-digital--sd--devices.md)
*  [USB 设备的标识符](identifiers-for-usb-devices.md)


 






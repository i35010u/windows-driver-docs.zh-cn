---
title: 步骤 1 的新设备标识
description: 步骤 1 的新设备标识
ms.assetid: e0df70ca-cea3-44a1-b5ff-407f72a216f9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 176fe9318ae5339fb42984174bf8f040458f9db6
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161523"
---
# <a name="step-1-the-new-device-is-identified"></a>第 1 步：标识新设备


新设备、 总线或中心驱动程序到安装了驱动程序之前它将设备连接分配[硬件标识符 (ID)](hardware-ids.md)到设备。 Windows 使用硬件 Id 来查找设备之间的最接近匹配和一个[驱动程序包](driver-packages.md)，其中包含设备的驱动程序。 有关硬件 Id 的详细信息，请参阅[设备标识字符串](device-identification-strings.md)。

硬件 ID 的格式通常包括以下：

-   总线特定的前缀，如 PCI\\或 USB\\。
-   该设备，如供应商、 型号和修订版本标识符的特定于供应商的标识符。 这些标识符内的硬件 ID 的格式也是特定于总线驱动程序。

独立硬件供应商 (IHV) 还可以定义一个或多个[兼容 Id](compatible-ids.md)设备。 兼容 Id 有相同的硬件 Id; 的格式但是，它们通常比硬件 Id 更通用，并且不需要特定制造商或型号信息。 Windows 使用这些标识符来选择[驱动程序包](driver-packages.md)设备如果操作系统找不到匹配的驱动程序包的设备的硬件 id。 Ihv 指定一个或多个兼容的驱动程序包中的设备 Id [INF 文件](overview-of-inf-files.md)。

Windows 使用硬件 Id 和兼容 Id 搜索[驱动程序包](driver-packages.md)设备。 查找匹配的驱动程序包的设备通过设备的硬件 Id 和兼容 Id 对这些 Id 的包中指定的比较[INF 文件](overview-of-inf-files.md)。

例如，当用户插入到的端口连接到计算机的 USB 集线器的无线局域网 (WLAN) 适配器，则执行以下步骤：

1.  USB 集线器驱动程序检测到该设备。 根据查询从适配器的信息，中心驱动程序创建设备的硬件 ID。

    例如，USB 集线器驱动程序可以创建硬件 ID 的 USB\\VID_1234 PID_5678 & REV_0001 WLAN 适配器，其中：

    -   VID_1234 是供应商的标识符。
    -   PID_5678 是设备的产品或模型中，标识符。
    -   REV_0001 是设备的修订版本标识符。

    有关 USB 的硬件 Id 的格式的详细信息，请参阅[USB 设备的标识符](identifiers-for-usb-devices.md)。

2.  USB 集线器驱动程序通知[插即用 (PnP) 管理器](pnp-manager.md)检测到新设备。 PnP 管理器将查询所有设备的硬件 Id 的中心驱动程序。 中心驱动程序可以创建同一个设备的多个硬件 Id。

3.  [PnP 管理器](pnp-manager.md)通知新设备需要安装 Windows。 作为此通知的一部分，Windows 附带的硬件 Id 列表。

4.  Windows 启动的搜索[驱动程序包](driver-packages.md)相匹配的设备硬件 Id 之一。 如果 Windows 找不到匹配的硬件 ID，它将搜索具有匹配的兼容 ID 的设备的驱动程序包。

    有关此过程的详细信息，请参阅[步骤 2:所选设备的驱动程序](step-2--a-driver-for-the-device-is-selected.md)。

每个总线驱动程序以其自身的、 特定于总线的方式构造的硬件 Id。

对于其他总线标准化标识符的示例，请参阅：

*  [PCI 设备的标识符](identifiers-for-pci-devices.md)
*  [SCSI 设备的标识符](identifiers-for-scsi-devices.md)
*  [IDE 设备标识符](identifiers-for-ide-devices.md)
*  [PCMCIA 设备标识符](identifiers-for-pcmcia-devices.md)
*  [适用于 ISAPNP 设备标识符](identifiers-for-isapnp-devices.md)
*  [1394 设备标识符](identifiers-for-1394-devices.md)
*  [安全数字 (SD) 设备的标识符](identifiers-for-secure-digital--sd--devices.md)
*  [USB 设备的标识符](identifiers-for-usb-devices.md)


 






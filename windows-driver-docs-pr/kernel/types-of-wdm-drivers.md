---
title: WDM 驱动程序的类型
description: 有三种类型的 WDM 驱动程序总线驱动程序、 函数驱动程序和筛选器驱动程序。
ms.assetid: 86acc77e-816e-46c8-b63c-2bb10920acd6
keywords:
- WDM 驱动程序 WDK 内核类型
- WDM 驱动程序 WDK 内核，分层驱动程序
- 分层驱动程序 WDK 内核
- 驱动程序层 WDK WDM
- 总线驱动程序 WDK WDM
- 函数的 WDK WDM 驱动程序
- 筛选器驱动程序 WDK WDM
- WDM 总线驱动程序 WDK
- WDM 函数驱动程序 WDK
- WDM 筛选器驱动程序 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b81d7cf1f0f7d31e9674d39a47a23439d20f8f7c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534384"
---
# <a name="types-of-wdm-drivers"></a>WDM 驱动程序的类型


有三种类型的 WDM 驱动程序： 总线驱动程序、 函数驱动程序和筛选器驱动程序。




-   一个[总线驱动程序](bus-drivers.md)推动单个 I/O 总线设备，并提供了与设备无关的每个插槽功能。 总线驱动程序还检测并报告连接到该总线的子设备。
-   一个[功能驱动程序](function-drivers.md)驱动器单个设备。
-   一个[筛选器驱动程序](filter-drivers.md)筛选设备、 设备、 类或总线的 I/O 请求。

在此上下文中，*总线*是向其附加其他物理、 逻辑，或虚拟设备; 总线包括 SCSI 和 PCI，还以并行端口的串行端口和 i8042 端口等传统的总线的任何设备。

非常重要的驱动程序开发人员若要了解不同种类的 WDM 驱动程序并了解他们所写哪种类型的驱动程序。 例如，是否将驱动程序处理每个[插](implementing-plug-and-play.md)IRP 以及如何处理此类 Irp 取决于哪种驱动程序正在编写 （总线驱动程序、 功能驱动程序或筛选器驱动程序）。

### <a href="" id="possible-driver-layers"></a>

下图显示了总线驱动程序、 功能驱动程序和设备的筛选器驱动程序之间的关系。

![说明可能的驱动程序层关系图](images/drvlyr.png)

每个设备通常具有父 I/O 总线、 设备功能驱动程序和零个或多个筛选器驱动程序的设备的总线驱动程序。 需要很多筛选器驱动程序的驱动程序设计不会产生最佳性能。

在上图中的驱动程序如下所示：

1.  一个*总线驱动程序*服务总线控制器、 适配器或桥。 总线驱动程序是必需的驱动程序;没有为每种类型的计算机上的总线的一个总线驱动程序。 Microsoft 提供了最常见的总线总线驱动程序。 Ihv 和 Oem 可以提供其他总线驱动程序。

2.  一个*总线筛选器驱动程序*通常将值添加到总线，并由 Microsoft 或 OEM 的系统提供。 可以有任意数量的总线筛选器驱动程序。

3.  *较低级别筛选器驱动程序*通常会修改设备硬件的行为。 它们是可选的通常由 Ihv 提供。 可以有任意数量的较低级别筛选器驱动程序的设备。

4.  一个*功能驱动程序*是设备的主要驱动程序。 功能驱动程序通常由设备供应商编写，并且需要 (除非该设备正在使用中，否则*raw 模式*)。

5.  *较高级别筛选器驱动程序*通常为设备提供添加值功能。 它们是可选的通常由 Ihv 提供。

下面的主题介绍三种常规类型的 WDM 驱动程序 — 总线驱动程序，功能的驱动程序，筛选器驱动程序 — 在详细信息。 此外包括是使用示例 USB 驱动程序的 WDM 驱动程序分层的示例。

## <a name="in-this-section"></a>本部分内容


-   [总线驱动程序](bus-drivers.md)
-   [功能的驱动程序](function-drivers.md)
-   [筛选器驱动程序](filter-drivers.md)
-   [WDM 驱动程序层：示例](wdm-driver-layers---an-example.md)

 

 





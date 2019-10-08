---
title: WDM 驱动程序的类型
description: 有三种 WDM 驱动程序总线驱动程序、函数驱动程序和筛选器驱动程序。
ms.assetid: 86acc77e-816e-46c8-b63c-2bb10920acd6
keywords:
- WDM 驱动程序 WDK 内核，类型
- WDM 驱动程序 WDK 内核，分层驱动程序
- 分层驱动程序 WDK 内核
- 驱动程序层 WDK WDM
- 总线驱动程序 WDK WDM
- 函数驱动程序 WDK WDM
- 筛选器驱动程序 WDK WDM
- WDM 总线驱动程序 WDK
- WDM 函数驱动程序 WDK
- WDM 筛选器驱动程序 WDK
ms.date: 06/16/2017
ms.localizationpriority: High
ms.openlocfilehash: 0bb3c681298fad8ccecdc35842e512058c350a70
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007652"
---
# <a name="types-of-wdm-drivers"></a>WDM 驱动程序的类型


有三种 WDM 驱动程序：总线驱动程序、函数驱动程序和筛选器驱动程序。




-   [总线驱动程序驱动](bus-drivers.md)单个 i/o 总线设备，并提供与设备无关的每个槽功能。 总线驱动程序还会检测并报告连接到总线的子设备。
-   [函数驱动程序](function-drivers.md)用于驱动单个设备。
-   [筛选器驱动程序](filter-drivers.md)对设备、设备类或总线的 i/o 请求进行筛选。

在此上下文中，*总线*是其他物理、逻辑或虚拟设备附加到的任何设备;总线包括传统总线，如 SCSI 和 PCI，以及并行端口、串行端口和 i8042 端口。

驱动程序开发人员必须了解不同类型的 WDM 驱动程序并知道他们正在编写哪种类型的驱动程序，这一点非常重要。 例如，驱动程序是否处理每个[即插即用](implementing-plug-and-play.md)IRP 以及如何处理此类 irp 取决于正在写入的驱动程序的类型（总线驱动程序、函数驱动程序或筛选器驱动程序）。

### <a href="" id="possible-driver-layers"></a>

下图显示了设备的总线驱动程序、函数驱动程序和筛选器驱动程序之间的关系。

![说明可能的驱动层的关系图](images/drvlyr.png)

每个设备通常具有适用于父 i/o 总线的总线驱动程序、设备的函数驱动程序以及设备的零个或多个筛选器驱动程序。 需要许多筛选器驱动程序的驱动程序设计并不能获得最佳性能。

上图中的驱动程序如下所示：

1.  *总线驱动程序*服务总线控制器、适配器或网桥。 总线驱动程序是必需的驱动程序;计算机上的每个总线类型都有一个总线驱动程序。 Microsoft 为大多数常见总线提供总线驱动程序。 Ihv 和 Oem 可以提供其他总线驱动程序。

2.  *总线筛选器驱动程序*通常会将值添加到总线，由 Microsoft 或系统 OEM 提供。 总线可以有任意数量的总线筛选器驱动程序。

3.  *较低级别的筛选器驱动程序*通常会修改设备硬件的行为。 它们是可选的，通常由 Ihv 提供。 一个设备可以有任意数量的低级筛选器驱动程序。

4.  *函数驱动程序*是设备的主驱动程序。 函数驱动程序通常由设备供应商编写，并且是必需的（除非设备正在*raw 模式下*使用）。

5.  *上层筛选器驱动程序*通常为设备提供附加的值功能。 它们是可选的，通常由 Ihv 提供。

以下主题详细说明了三种类型的 WDM 驱动程序：总线驱动程序、函数驱动程序和筛选器驱动程序。 还包括使用示例 USB 驱动程序的 WDM 驱动程序层的示例。

## <a name="in-this-section"></a>本节内容


-   [总线驱动程序](bus-drivers.md)
-   [函数驱动程序](function-drivers.md)
-   [筛选器驱动程序](filter-drivers.md)
-   @no__t 0WDM 驱动程序层：一个示例 @ no__t-0

 

 





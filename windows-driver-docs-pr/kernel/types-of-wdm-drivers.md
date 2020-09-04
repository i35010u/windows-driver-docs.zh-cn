---
title: WDM 驱动程序的类型
description: 有三种类型的 WDM 驱动程序：总线驱动程序、函数驱动程序和筛选器驱动程序。
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
ms.openlocfilehash: fb163074078c0925df90b66edda42df6a69c9ba1
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402848"
---
# <a name="types-of-wdm-drivers"></a>WDM 驱动程序的类型


有三种类型的 WDM 驱动程序：总线驱动程序、函数驱动程序和筛选器驱动程序。




-   [总线驱动程序](bus-drivers.md)驱动单个 I/O 总线设备，并提供与设备无关的单槽功能。 总线驱动程序还检测并报告连接到总线的子设备。
-   [函数驱动程序](function-drivers.md)驱动单个设备。
-   [筛选器驱动程序](filter-drivers.md)筛选设备的 I/O 请求、设备类或总线。

在此上下文中，*总线*是其他物理、逻辑或虚拟设备连接到的任何设备；总线包括传统总线（如 SCSI 和 PCI）以及并行端口、串行端口和 i8042 端口。

驱动程序开发人员必须了解不同类型的 WDM 驱动程序并知道自己正在编写哪种类型的驱动程序，这一点非常重要。 例如，驱动程序是否处理每个[即插即用](introduction-to-plug-and-play.md) IRP 以及如何处理此类 IRP 取决于所编写的驱动程序的类型（总线驱动程序、函数驱动程序或筛选器驱动程序）。

### <a href="" id="possible-driver-layers"></a>

下图显示了设备的总线驱动程序、函数驱动程序和筛选器驱动程序之间的关系。

![关系图，演示可能的驱动程序层](images/drvlyr.png)

每个设备通常都有针对父 I/O 总线的总线驱动程序、针对设备的函数驱动程序，以及零个或零个以上针对设备的筛选器驱动程序。 需要许多筛选器驱动程序的驱动程序设计不会获得最佳性能。

上图中的驱动程序详述如下：

1.  总线驱动程序  为总线控制器、适配器或桥提供服务。 总线驱动程序是必需的驱动程序；计算机上的每个总线类型都有一个总线驱动程序。 Microsoft 为大多数常见总线提供总线驱动程序。 IHV 和 OEM 可以提供其他总线驱动程序。

2.   总线筛选器驱动程序通常会将值添加到总线，由 Microsoft 或系统 OEM 提供。 一个总线可以有任意数量的总线筛选器驱动程序。

3.   底层筛选器驱动程序通常修改设备硬件的行为。 它们是可选的，通常由 IHV 提供。 一个设备可以有任意数量的底层筛选器驱动程序。

4.  函数驱动程序  是设备的主驱动程序。 函数驱动程序通常由设备供应商编写，并且是必需的（除非在原始模式  下使用设备）。

5.  上层筛选器驱动程序  通常为设备提供增值功能。 它们是可选的，通常由 IHV 提供。

以下主题详细说明了三种常规类型的 WDM 驱动程序：总线驱动程序、函数驱动程序、筛选器驱动程序。 另外还包括了一个使用示例 USB 驱动程序的 WDM 驱动程序分层的示例。

## <a name="in-this-section"></a>本部分内容


-   [总线驱动程序](bus-drivers.md)
-   [函数驱动程序](function-drivers.md)
-   [筛选器驱动程序](filter-drivers.md)
-   [WDM 驱动程序层：示例](wdm-driver-layers---an-example.md)

 

 





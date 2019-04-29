---
title: NDIS 6.40 简介
description: 本部分介绍 NDIS 6.40 并描述其主要设计新增功能。 在 Windows 8.1 和 Windows Server 2012 R2 和更高版本的 NDIS 6.40。
ms.assetid: 46DB94AA-DBAD-49E0-A1F0-FEB095E26F2C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4d3253b9acb6a29120d31915b067efca58c421a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380607"
---
# <a name="introduction-to-ndis-640"></a>NDIS 6.40 简介


本部分介绍网络驱动程序接口规范 (NDIS) 6.40 并描述其主要设计新增功能。 NDIS 6.40 包含在 Windows 8.1 和 Windows Server 2012 R2 和更高版本操作系统中。

## <a name="feature-updates"></a>功能更新


Windows 8.1 和 Windows Server 2012 R2 引入了以下功能的次要更新：

### <a name="ndkpi"></a>NDKPI

NDKPI 1.2 将以下新元素添加到 NDKPI DDI:

- *NdkSendAndInvalidate* ([*NDK\_FN\_发送\_AND\_INVALIDATE*](https://msdn.microsoft.com/library/windows/hardware/dn265507)) 函数
- *NdkGetCqResultsEx* ([*NDK\_FN\_获取\_CQ\_结果\_EX*](https://msdn.microsoft.com/library/windows/hardware/dn265506)) 函数
- [**NDK\_结果\_EX** ](https://msdn.microsoft.com/library/windows/hardware/dn265509)结构
- 新的请求回调*标志*值：**NDK\_OP\_FLAG\_DEFER**
- 新[ **NDK\_适配器\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh439851)**AdapterFlags**值：**NDK\_适配器\_标志\_RDMA\_读取\_本地\_INVALIDATE\_支持**

### <a name="native-80211-wireless-lan"></a>本机 802.11 无线 LAN

IEEE 802.11 a c 现在支持最高吞吐量 (VHT) PHY。 已更新以下 DDI 元素：

- [**DOT11\_PHY\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff548741)枚举
- [OID\_DOT11\_当前\_通道](https://msdn.microsoft.com/library/windows/hardware/ff569127)
- [OID\_DOT11\_支持\_PHY\_类型](https://msdn.microsoft.com/library/windows/hardware/ff569426)
- [OID\_DOT11\_SUPPORTED\_OFDM\_FREQUENCY\_LIST](https://msdn.microsoft.com/library/windows/hardware/ff569425)

## <a name="sample-and-documentation-updates"></a>示例和文档更新

[转发扩展插件示例的 HYPER-V 可扩展交换机](https://go.microsoft.com/fwlink/p/?LinkId=617913)已更新，以实现混合转发。

以下文档部分已添加或显著扩展：

-   [移植到 NDIS 6.30 NDIS 6.x 驱动程序](porting-ndis-6-x-drivers-to-ndis-6-30.md)
-   [网络直接内核提供程序接口 (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)设计指南
-   [使用通用路由封装 (NVGRE) 任务卸载的网络虚拟化](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)
-   [接收段合并 (RSC)](receive-segment-coalescing--rsc-.md)设计指南
-   [编写入门的 HYPER-V 可扩展交换机扩展](getting-started-writing-a-hyper-v-extensible-switch-extension.md)
-   [NVGRE 任务卸载参考](https://msdn.microsoft.com/library/windows/hardware/dn197221)

NetDMA 接口不支持在 Windows 8 和 Windows Server 2012 及更高版本。 文档现已更新以反映此。

本部分包括以下主题：

- [实现 6.40 NDIS 驱动程序](implementing-an-ndis-6-40-driver.md)
- [使用 NDIS 6.40 数据结构](using-ndis-6-40-data-structures.md)
- [编译 6.40 NDIS 驱动程序](compiling-an-ndis-6-40-driver.md)

 

 






---
title: NDIS 6.40 简介
description: 本部分介绍了 NDIS 6.40，并介绍了其主要的设计添加内容。 Windows 8.1 和 Windows Server 2012 R2 及更高版本中都包含 NDIS 6.40。
ms.assetid: 46DB94AA-DBAD-49E0-A1F0-FEB095E26F2C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 934417f92d978fe513a5298c6ec71c2a9b90a789
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844172"
---
# <a name="introduction-to-ndis-640"></a>NDIS 6.40 简介


本部分介绍网络驱动程序接口规范（NDIS）6.40，并介绍其主要的设计添加内容。 Windows 8.1 和 Windows Server 2012 R2 及更高版本的操作系统中都包含 NDIS 6.40。

## <a name="feature-updates"></a>功能更新


Windows 8.1 和 Windows Server 2012 R2 引入了以下功能的次要更新：

### <a name="ndkpi"></a>NDKPI

NDKPI 1.2 将以下新元素添加到 NDKPI DDI：

- *NdkSendAndInvalidate* （[*NDK\_FN\_发送\_和\_无效*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_send_and_invalidate)）函数
- *NdkGetCqResultsEx* （[*NDK\_FN\_获取\_CQ\_结果\_EX*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_get_cq_results_ex)）函数
- [**NDK\_结果\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_result_ex)结构
- 新请求回调*标志*值： **NDK\_OP\_标志\_延迟**
- 新[**NDK\_适配器\_信息**](https://docs.microsoft.com/windows/desktop/api/ndkinfo/ns-ndkinfo-_ndk_adapter_info)**AdapterFlags**值： **NDK\_适配器\_标志\_RDMA\_读取\_本地\_无效\_支持**

### <a name="native-80211-wireless-lan"></a>本机802.11 无线 LAN

目前支持 IEEE 802.11 ac 极高吞吐量（VHT） PHY。 已更新以下 DDI 元素：

- [**DOT11\_PHY\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/windot11/ne-windot11-_dot11_phy_type)枚举
- [OID\_DOT11\_当前\_通道](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-current-channel)
- [OID\_DOT11\_支持的\_PHY\_类型](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-supported-phy-types)
- [OID\_DOT11\_支持\_OFDM\_频率\_列表](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-supported-ofdm-frequency-list)

## <a name="sample-and-documentation-updates"></a>示例和文档更新

已更新[Hyper-v 可扩展交换机转发扩展示例](https://go.microsoft.com/fwlink/p/?LinkId=617913)以实现混合转发。

以下文档部分已添加或明显展开：

-   [将 NDIS 1.x 驱动程序移植到 NDIS 6.30](porting-ndis-6-x-drivers-to-ndis-6-30.md)
-   [网络直接内核提供程序接口（NDKPI）](network-direct-kernel-programming-interface--ndkpi-.md)设计指南
-   [使用通用路由封装（NVGRE）任务卸载的网络虚拟化](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)
-   [接收段合并（RSC）](receive-segment-coalescing--rsc-.md)设计指南
-   [编写 Hyper-v 可扩展交换机扩展入门](getting-started-writing-a-hyper-v-extensible-switch-extension.md)
-   [NVGRE 任务卸载参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

Windows 8 和 Windows Server 2012 及更高版本不支持 NetDMA 接口。 文档现已更新以反映此情况。

本部分包括下列主题：

- [实现 NDIS 6.40 驱动程序](implementing-an-ndis-6-40-driver.md)
- [使用 NDIS 6.40 数据结构](using-ndis-6-40-data-structures.md)
- [编译 NDIS 6.40 驱动程序](compiling-an-ndis-6-40-driver.md)

 

 






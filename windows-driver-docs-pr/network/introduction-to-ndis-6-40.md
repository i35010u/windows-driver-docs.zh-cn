---
title: NDIS 6.40 简介
description: 本部分介绍了 NDIS 6.40，并介绍了其主要的设计添加内容。 Windows 8.1 和 Windows Server 2012 R2 及更高版本中都包含 NDIS 6.40。
ms.assetid: 46DB94AA-DBAD-49E0-A1F0-FEB095E26F2C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73e1700980c289f98aec5fae11b790ad01c96a7c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215616"
---
# <a name="introduction-to-ndis-640"></a>NDIS 6.40 简介


本部分介绍 (NDIS) 6.40 的网络驱动程序接口规格，并介绍了其主要的设计添加。 Windows 8.1 和 Windows Server 2012 R2 及更高版本的操作系统中都包含 NDIS 6.40。

## <a name="feature-updates"></a>功能更新


Windows 8.1 和 Windows Server 2012 R2 引入了以下功能的次要更新：

### <a name="ndkpi"></a>NDKPI

NDKPI 1.2 将以下新元素添加到 NDKPI DDI：

- *NdkSendAndInvalidate* ([*NDK \_ FN \_ SEND \_ 并 \_ 使*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_send_and_invalidate)) 函数无效
- *NdkGetCqResultsEx* ([*NDK \_ FN \_ GET \_ CQ \_ 结果， \_ 如*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_get_cq_results_ex)) 函数
- [**NDK \_结果 \_ EX**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_result_ex) 结构
- 新请求回调 *标志* 值： **NDK \_ 操作 \_ 标志 \_ 延迟**
- 新 [**NDK \_ 适配器 \_ 信息**](/windows/desktop/api/ndkinfo/ns-ndkinfo-_ndk_adapter_info)**AdapterFlags** 值： **ndk \_ 适配器 \_ 标志 \_ RDMA \_ 支持 RDMA 读取 \_ 本地 \_ 无效 \_ **

### <a name="native-80211-wireless-lan"></a>本机802.11 无线 LAN

IEEE 802.11 ac 极高的吞吐量 (VHT) PHY 现在受支持。 已更新以下 DDI 元素：

- [**DOT11 \_PHY \_ 类型**](/windows-hardware/drivers/ddi/windot11/ne-windot11-_dot11_phy_type) 枚举
- [OID \_ DOT11 \_ 当前 \_ 通道](/previous-versions/windows/hardware/wireless/oid-dot11-current-channel)
- [OID \_ DOT11 \_ 支持的 \_ PHY \_ 类型](/previous-versions/windows/hardware/wireless/oid-dot11-supported-phy-types)
- [OID \_ DOT11 \_ 支持 \_ OFDM \_ FREQUENCY \_ 列表](/previous-versions/windows/hardware/wireless/oid-dot11-supported-ofdm-frequency-list)

## <a name="sample-and-documentation-updates"></a>示例和文档更新

已更新 [Hyper-v 可扩展交换机转发扩展示例](https://go.microsoft.com/fwlink/p/?LinkId=617913) 以实现混合转发。

以下文档部分已添加或明显展开：

-   [将 NDIS 6.x 驱动程序移植到 NDIS 6.30](porting-ndis-6-x-drivers-to-ndis-6-30.md)
-   [网络直接内核提供程序接口 (NDKPI) ](./overview-of-network-direct-kernel-provider-interface--ndkpi-.md) 设计指南
-   [使用通用路由封装 (NVGRE) 任务卸载实现网络虚拟化](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)
-   [ (RSC) 接收段合并 ](receive-segment-coalescing--rsc-.md) 设计指南
-   [开始编写 Hyper-V 可扩展交换机扩展](getting-started-writing-a-hyper-v-extensible-switch-extension.md)
-   [NVGRE 任务卸载参考](/windows-hardware/drivers/ddi/_netvista/)

Windows 8 和 Windows Server 2012 及更高版本不支持 NetDMA 接口。 文档现已更新以反映此情况。

本节包括下列主题：

- [实现 NDIS 6.40 驱动程序](implementing-an-ndis-6-40-driver.md)
- [使用 NDIS 6.40 数据结构](using-ndis-6-40-data-structures.md)
- [编译 NDIS 6.40 驱动程序](compiling-an-ndis-6-40-driver.md)

 


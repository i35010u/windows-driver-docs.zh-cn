---
title: 有关管理数据包合并接收筛选器的指导
description: 有关管理数据包合并接收筛选器的指导
ms.assetid: 7FA44368-1641-478A-927B-020619F39A0D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1274d1f9c2f56c90155dfcf26f86920d49c506f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217624"
---
# <a name="guidelines-for-managing-packet-coalescing-receive-filters"></a>有关管理数据包合并接收筛选器的指导


如果微型端口驱动程序支持 NDIS 数据包合并，则必须遵循这些准则来管理包合并接收筛选器：

-   微型端口驱动程序和基础网络适配器必须能够动态地处理接收筛选器的设置和清除。 可以随时设置或清除各个接收筛选器。

-   微型端口驱动程序必须保留合并的数据包计数器。 此64位计数器包含与数据包合并筛选器匹配的已接收数据包数的值。 NDIS 通过 oid [ \_ 数据包 \_ 合并 \_ 筛选器 \_ 匹配 \_ 计数](./oid-packet-coalescing-filter-match-count.md)的 oid 查询请求来查询此计数器。

    **注意**   微型端口驱动程序通过处理[oid \_ PNP \_ 设置 \_ 功能](./oid-pnp-set-power.md)的 oid 集请求来在转换为全电源状态时清除此计数器。 调用 [*MiniportResetEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset) 函数时，微型端口驱动程序还会清除计数器。

     

-   小型端口驱动程序在转换为低功率状态时不得丢弃数据包合并接收筛选器。 但是，当网络适配器处于低功耗状态时，它必须仅根据已通过 OID 设置 [oid \_ PNP \_ ENABLE \_ 唤醒 \_ 启用](./oid-pnp-enable-wake-up.md)的唤醒模式筛选接收的数据包。

    当适配器转换为完全电源状态时，微型端口驱动程序必须将网络适配器配置为具有数据包合并接收筛选器。

-   当 NDIS 调用驱动程序的 [*MiniportResetEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset) 函数时，微型端口驱动程序不得丢弃数据包合并接收筛选器。 驱动程序重置网络适配器后，必须将该适配器配置为具有数据包合并筛选器。 而且，驱动程序 *必须清除* 合并的数据包计数器。

    **注意**   无论驱动程序是否将*AddressingReset*参数设置为 TRUE，微型端口驱动程序都必须执行此操作。

     

-   如果微型端口驱动程序在本机802.11 可扩展工作站 (ExtSTA) 模式下运行，则它在处理 [oid \_ DOT11 \_ 重置 \_ 请求](/previous-versions/windows/hardware/wireless/oid-dot11-reset-request)的 oid 方法请求时不得丢弃数据包合并接收筛选器。 在微型端口驱动程序执行802.11 重置操作后，必须将网络适配器配置为具有数据包合并接收筛选器。 而且，驱动程序 *不能清除* 合并的数据包计数器。

    有关本机802.11 可扩展工作站模式的详细信息，请参阅 [可扩展工作站操作模式](/previous-versions/windows/hardware/wireless/extensible-station-operation-mode)。

    **注意**   对于在可扩展访问点 (ExtAP) 模式下运行的本机802.11 微型端口驱动程序，NDIS 不支持数据包合并。 有关 ExtAP 操作模式的详细信息，请参阅 [可扩展访问点操作模式](/previous-versions/windows/hardware/wireless/extensible-access-point-operation-mode)。

     

 


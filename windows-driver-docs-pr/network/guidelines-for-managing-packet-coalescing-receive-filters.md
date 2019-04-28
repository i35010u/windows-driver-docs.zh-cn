---
title: 有关管理数据包合并接收筛选器的指导
description: 有关管理数据包合并接收筛选器的指导
ms.assetid: 7FA44368-1641-478A-927B-020619F39A0D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d2c9655df84ae976963836f28dd02afea5d2580
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349863"
---
# <a name="guidelines-for-managing-packet-coalescing-receive-filters"></a>有关管理数据包合并接收筛选器的指导


如果微型端口驱动程序支持 NDIS 数据包合并，它必须遵循这些指导原则，用于管理数据包合并接收筛选器：

-   必须能够处理设置的微型端口驱动程序和基础网络适配器和交换的接收动态筛选器。 单个接收筛选器可能会设置或清除在任何时间。

-   微型端口驱动程序必须维护一个合并的数据包的计数器。 此 64 位计数器包含具有匹配的数据包的合并筛选器的接收数据包数的值。 NDIS 查询通过 OID 查询请求的此计数器[OID\_数据包\_COALESCING\_筛选器\_匹配\_计数](https://msdn.microsoft.com/library/windows/hardware/hh451826)。

    **请注意**  微型端口驱动程序时它将转换为全功率状态处理的一个 OID 集请求通过清除此计数器[OID\_PNP\_设置\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)。 微型端口驱动程序还会清除计数器时其[ *MiniportResetEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559432)调用函数。

     

-   微型端口驱动程序必须放弃数据包时它将转换为低功耗状态合并接收筛选器。 但是，低功耗状态的网络适配器时，它必须仅筛选收到的数据包，基于已卸载到通过 OID 集请求的适配器的唤醒模式[OID\_PNP\_启用\_唤醒\_向上](https://msdn.microsoft.com/library/windows/hardware/ff569775)。

    微型端口驱动程序必须配置网络适配器在数据包合并筛选器时接收适配器将转换为全功率状态。

-   微型端口驱动程序必须放弃数据包时 NDIS 调用驱动程序的合并接收筛选器[ *MiniportResetEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559432)函数。 该驱动程序将重置网络适配器后，它必须与数据包合并筛选器来配置适配器。 此外，驱动程序*必须清除*合并的数据包计数器。

    **请注意**  微型端口驱动程序必须执行此操作而不考虑该驱动程序的设置是否*AddressingReset*参数设为 TRUE。

     

-   如果在本机 802.11 可扩展工作站 (ExtSTA) 模式下运行时的微型端口驱动程序，它必须不丢弃数据包时处理 OID 方法请求的合并接收筛选器[OID\_DOT11\_重置\_请求](https://msdn.microsoft.com/library/windows/hardware/ff569409)。 微型端口驱动程序执行 802.11 重置操作后，它必须配置网络适配器合并接收数据包与筛选器。 此外，驱动程序*必须清除*合并的数据包计数器。

    有关本机 802.11 可扩展工作站模式下的详细信息，请参阅[可扩展工作站操作模式下](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/extensible-station-operation-mode)。

    **请注意**  NDIS 不支持数据包合并本机 802.11 微型端口驱动程序操作中可扩展的访问点 (ExtAP) 模式。 有关 ExtAP 操作模式的详细信息，请参阅[可扩展访问点操作模式](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/extensible-access-point-operation-mode)。

     

 

 






---
title: 微型端口适配器 OID 请求序列化
description: 微型端口适配器 OID 请求序列化
keywords:
- Oid WDK 网络，微型端口适配器请求
- 小型端口适配器 WDK 网络，OID 请求
- 适配器 WDK 网络，OID 请求
- 对象标识符 WDK 网络
- OID 序列化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5162d114c06281be81db9b825f46beec414e746e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218011"
---
# <a name="miniport-adapter-oid-request-serialization"></a>微型端口适配器 OID 请求序列化

对微型端口适配器的所有 OID 请求均由 NDIS 序列化，但不会对 [直接 OID 请求](miniport-adapter-direct-oid-requests.md)进行序列化。 在完成任何挂起的请求之前，微型端口适配器将不会收到新的 OID 请求。 因此，小型端口适配器必须立即完成 Oid。

>[!NOTE]
> 建议在小于1000毫秒的情况下或1秒内完成 OID 请求，以使用户不会注意到任何性能延迟。 有关计时 OID 请求的特定信息，请参阅 [NdisTimedOidComplete](../devtest/ndis-ndistimedoidcomplete.md) 驱动程序验证程序规则。

此 OID 序列化规则的一个例外是适用于使用 WDI 的 Wi-fi 微型端口适配器，如果这些适配器的时间太长而无法完成以前的 OID，它可能会看到另一个 OID 请求。 下面的示例说明了在这种情况下会发生什么情况：

1. 第一个 OID 请求会传递到 WDI 微型端口适配器。
2. NIC 在驱动程序指定的时间限制内未响应 OID。
3. WDI 调用驱动程序的 [MINIPORT_WDI_ADAPTER_HANG_DIAGNOSE](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_adapter_hang_diagnose) 回调函数来收集有关 NIC 的诊断数据。
4. 第一个 OID 不再被视为阻止序列化。 这意味着 WDI 微型端口适配器现在可以接收其他 OID 请求，即使第一个 OID 是序列化的。 不过，还会对这些其他 OID 进行序列化，这意味着 WDI 微型端口适配器将不会同时挂起2个以上的 Oid (第一个仍挂起的 OID，另一个 OID) 。

## <a name="related-topics"></a>相关主题

有关 WDI UE 挂机检测的详细信息，请参阅 [ue 挂检测：步骤 1-14](./wdi-ue-hang-detection--step-1-to-step-14.md)。

有关 NDIS 中 OID 请求的详细信息，请参阅在 NDIS 博客上 [简化 oid 请求处理程序](https://go.microsoft.com/fwlink/p/?linkid=846658) 。
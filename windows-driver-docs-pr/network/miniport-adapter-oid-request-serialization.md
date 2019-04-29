---
title: 微型端口适配器 OID 请求序列化
description: 微型端口适配器 OID 请求序列化
keywords:
- Oid WDK 网络、 微型端口适配器请求
- 微型端口适配器 WDK 网络、 OID 请求
- 适配器 WDK 网络、 OID 请求
- 对象标识符 WDK 网络
- OID 序列化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 754f58065f8cb264cd5a6230b17c87433ff60138
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372496"
---
# <a name="miniport-adapter-oid-request-serialization"></a>微型端口适配器 OID 请求序列化

微型端口适配器的所有 OID 请求都序列化除 NDIS [OID 请求定向](miniport-adapter-direct-oid-requests.md)，这设计不会序列都化。 微型端口适配器不会收到新的 OID 请求，直到完成任何挂起的请求。 因此，微型端口适配器必须立即完成 Oid。

>[!NOTE]
> 我们建议您完成在小于 1000 毫秒或 1 秒的 OID 请求，因此用户不会注意到性能中的任何延迟。 有关计时 OID 请求的特定信息，请参阅[NdisTimedOidComplete](https://msdn.microsoft.com/library/windows/hardware/dn305120)驱动程序验证程序规则。

此 OID 序列化规则的例外是适用于使用 WDI，可能会看到第二个 OID 请求，如果它们花费很长时间才能完成以前的 OID 的 Wi-fi 微型端口适配器。 下面的示例介绍了在此情况下会发生什么情况：

1. 第一个 OID 请求传递到 WDI 微型端口适配器。
2. NIC 不响应由驱动程序指定的时间限制内的 OID。
3. WDI 调用驱动程序的[MINIPORT_WDI_ADAPTER_HANG_DIAGNOSE](https://msdn.microsoft.com/library/windows/hardware/mt297558)回调函数来收集有关 NIC 的诊断数据
4. 第一个 OID 不再被视为阻止序列化。 这意味着 WDI 微型端口适配器现在可获得其他 OID 请求，即使第一个 OID 序列化。 但是，这些其他 OID 也会序列，这意味着 WDI 微型端口适配器将挂起 2 个以上的 Oid 同时 （仍然挂起的第一个 OID 和第二个 OID）。

## <a name="related-topics"></a>相关主题

有关 WDI UE 挂起检测的详细信息，请参阅[UE 挂起检测：步骤 1-14](https://msdn.microsoft.com/windows/hardware/drivers/network/wdi-ue-hang-detection--step-1-to-step-14)。

有关在 NDIS OID 请求的详细信息，请参阅[简化 OID 请求处理程序](https://go.microsoft.com/fwlink/p/?linkid=846658)NDIS 博客上。


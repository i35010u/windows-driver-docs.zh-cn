---
title: NDIS 支持的 WMI 操作
description: NDIS 支持的 WMI 操作
keywords:
- Windows Management Instrumentation WDK 网络，NDIS 操作
- WMI WDK 网络，NDIS 操作
- 虚拟连接 WDK NDIS WMI
- VCs WDK NDIS WMI
- 微型端口适配器 WDK 网络，枚举
- 适配器 WDK 网络，枚举
- 阳
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7c3e2cb9802c3158dc002ec0c695c3b37aae2a2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812985"
---
# <a name="ndis-supported-wmi-operations"></a>NDIS 支持的 WMI 操作





NDIS 支持以下 WMI 操作：

-   枚举适配器并枚举虚拟连接 (VC) 。

    NDIS 将全局 Guid 注册 ( [guid \_ ndis \_ 枚举 \_ 适配器 \_ EX](./guid-ndis-enumerate-adapters-ex.md) 和 GUID \_ ndis \_ 枚举 \_ VC) 使用 wmi 枚举 VC，使 wmi 客户端可以枚举所有微型端口适配器 (即微型端口驱动程序实例) 和所有命名的 VCs。 因为 NDIS 跟踪所有已加载的微型端口驱动程序和所有命名的 VCs，NDIS 不会查询微型端口驱动程序以获取此类信息。

-   查询单一实例并设置单个实例

    通过 NDIS，WMI 客户端可以查询或设置数据块的单个实例，该实例对应于单个 OID。 对于查询，NDIS 返回与适配器或 VC 关联的所有信息。 WMI 客户端无法查询或设置 OID 内的数据项。 例如，GUID \_ NDIS \_ GEN \_ 共同 \_ 链接 \_ 速度 guid 的查询同时返回出站和入站速度。 WMI 客户端无法仅查询出站速度或仅查询入站速度。

-   查询所有数据

    NDIS 通过获取相应的数据，并将 GUID 的所有实例的组合数据返回到 WMI，满足对特定 GUID 的所有数据请求的查询。 例如，对于 [GUID \_ NDIS \_ 枚举 \_ 适配器 \_ ](./guid-ndis-enumerate-adapters-ex.md)上的查询所有数据请求，ndis 会将所有已加载的微型端口驱动程序的列表返回到 WMI。 对于查询 GUID 上映射到 OID \_ GEN GEN XMIT pdu 的所有 \_ 数据 \_ \_ \_ ，NDIS 将在每个面向连接的微型端口驱动程序上查询每个 VC 的 OID，并将合并的数据返回到 WMI。 由于查询的开销可能很高，因此 WMI 客户端应使用 "仅查询所有数据" 请求来枚举适配器和 VCs。 确定适配器或 VC 兴趣后，客户端可以查询单个 GUID 实例。

-   EVENT NOTIFICATION

    WMI 客户端可以向 NDIS 注册，以接收特定状态指示的通知。 发生这种状态指示时，NDIS 会将状态信息与相应的 GUID 传递到 WMI，以便作为 WMI 事件传递到客户端。

-   EXECUTE 方法

    通过 NDIS，WMI 客户端可以运行与数据块关联的方法，该数据块对应于单个 OID。 WMI 客户端提供 NDIS 运行方法所需的信息。 方法请求可以与微型端口适配器、NDIS 端口或 VCs 关联。 方法成功运行后，NDIS 返回结果信息。

 


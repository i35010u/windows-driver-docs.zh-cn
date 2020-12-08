---
title: NDIS 网络接口 OID
description: 本部分介绍所有 NDIS 驱动程序的网络接口 Oid
keywords:
- NDIS 网络接口 OID
- WDK NDIS 网络接口 Oid
- WDK 网络接口 Oid
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70844cb49ff35976deabc2d917c4887ff87f19f8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825059"
---
# <a name="ndis-network-interface-oids"></a>NDIS 网络接口 OID

 (Oid 的 NDIS 网络接口对象标识符) 提供有关支持 MIB ([RFC 2863](overview-of-ndis-network-interfaces.md)) 的网络接口的信息。

NDIS 接口提供程序必须支持这些 Oid。 未注册接口提供程序的驱动程序不应支持本节中的 Oid。

NDIS 调用 [ProviderQueryObject](/windows-hardware/drivers/ddi/ndis/nc-ndis-if_query_object) 函数来发出查询请求，以获取接口提供程序的信息。 此函数的 *ObjectId* 参数包含对象标识符。 接口提供程序在调用 [NdisIfRegisterProvider](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterprovider)函数以注册为接口提供程序时注册了 *ProviderQueryObject* 。

*ProviderQueryObject* 函数的 *ProviderIfContext* 参数处的句柄标识网络接口。 此句柄是在接口提供程序调用 [NdisIfRegisterInterface](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface) 函数以注册接口时提供给 NDIS 的。 *ProviderQueryObject* 函数的 *POUTPUTBUFFER* 参数包含 OID 请求的结果。

有关 NDIS 网络接口 Oid 的详细信息，请参阅 [ndis 6.0 网络接口](ndis-network-interfaces2.md)。

本部分介绍以下 NDIS 网络接口 Oid：

- [OID_GEN_ALIAS](./oid-gen-alias.md) 
- [OID_GEN_ADMIN_STATUS](./oid-gen-admin-status.md) 
- [OID_GEN_OPERATIONAL_STATUS](./oid-gen-operational-status.md) 
- [OID_GEN_PROMISCUOUS_MODE](./oid-gen-promiscuous-mode.md) 
- [OID_GEN_XMIT_LINK_SPEED](./oid-gen-xmit-link-speed.md) 
- [OID_GEN_RCV_LINK_SPEED](./oid-gen-rcv-link-speed.md) 
- [OID_GEN_UNKNOWN_PROTOS](./oid-gen-unknown-protos.md) 
- [OID_GEN_DISCONTINUITY_TIME](./oid-gen-discontinuity-time.md) 
- [OID_GEN_LAST_CHANGE](./oid-gen-last-change.md) 
- [OID_GEN_INTERFACE_INFO](./oid-gen-interface-info.md) 
- [OID_GEN_MEDIA_CONNECT_STATUS_EX](./oid-gen-media-connect-status-ex.md) 
- [OID_GEN_LINK_SPEED_EX](./oid-gen-link-speed-ex.md) 
- [OID_GEN_MEDIA_DUPLEX_STATE](./oid-gen-media-duplex-state.md) 
- [OID_TUNNEL_INTERFACE_RELEASE_OID](./oid-tunnel-interface-release-oid.md) 
- [OID_TUNNEL_INTERFACE_SET_OID](./oid-tunnel-interface-set-oid.md)

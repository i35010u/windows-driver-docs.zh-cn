---
title: NDIS 网络接口 OID
description: 本部分介绍了所有的 NDIS 驱动程序的网络接口 Oid
keywords:
- NDIS 网络接口 OID
- WDK NDIS 网络接口 Oid
- WDK 网络接口 Oid
ms.assetid: A66B5AC6-9EAF-4234-8614-0EBF179B3DDE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d43d086e381f0eb4ecbaae1d4825a33ad316b1b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354982"
---
# <a name="ndis-network-interface-oids"></a>NDIS 网络接口 OID

NDIS 网络接口对象标识符 (Oid) 提供了有关支持的 MIB 的网络接口的信息 ([RFC 2863](overview-of-ndis-network-interfaces.md))。

NDIS 接口提供程序必须支持这些 Oid。 在本部分中，不是已注册的接口提供程序的驱动程序应支持 Oid。

NDIS 调用[ProviderQueryObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-if_query_object)函数来从接口提供程序发出查询请求的信息。 *ObjectId*此函数的参数包含的对象标识符。 接口提供程序注册*ProviderQueryObject*调用时[NdisIfRegisterProvider](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifregisterprovider)函数注册为接口提供程序。

在句柄*ProviderIfContext*的参数*ProviderQueryObject*函数标识的网络接口。 接口提供程序中调用时，此句柄已提供到 NDIS [NdisIfRegisterInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifregisterinterface)函数来注册接口。 *POutputBuffer*的参数*ProviderQueryObject*函数包含 OID 请求的结果。

网络接口 Oid 的 NDIS 有关的详细信息，请参阅[NDIS 6.0 网络接口](ndis-network-interfaces2.md)。

本部分介绍以下的 NDIS 网络接口 Oid:

- [OID_GEN_ALIAS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-alias) 
- [OID_GEN_ADMIN_STATUS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-admin-status) 
- [OID_GEN_OPERATIONAL_STATUS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-operational-status) 
- [OID_GEN_PROMISCUOUS_MODE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-promiscuous-mode) 
- [OID_GEN_XMIT_LINK_SPEED](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-link-speed) 
- [OID_GEN_RCV_LINK_SPEED](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-link-speed) 
- [OID_GEN_UNKNOWN_PROTOS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-unknown-protos) 
- [OID_GEN_DISCONTINUITY_TIME](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-discontinuity-time) 
- [OID_GEN_LAST_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-last-change) 
- [OID_GEN_INTERFACE_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-interface-info) 
- [OID_GEN_MEDIA_CONNECT_STATUS_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-connect-status-ex) 
- [OID_GEN_LINK_SPEED_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed-ex) 
- [OID_GEN_MEDIA_DUPLEX_STATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-duplex-state) 
- [OID_TUNNEL_INTERFACE_RELEASE_OID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tunnel-interface-release-oid) 
- [OID_TUNNEL_INTERFACE_SET_OID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tunnel-interface-set-oid) 



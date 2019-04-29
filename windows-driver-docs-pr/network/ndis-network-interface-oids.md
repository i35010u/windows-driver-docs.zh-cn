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
ms.openlocfilehash: 6d2a026cb2a86460b506fd55c0ca4036d6cb4641
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378345"
---
# <a name="ndis-network-interface-oids"></a>NDIS 网络接口 OID

NDIS 网络接口对象标识符 (Oid) 提供了有关支持的 MIB 的网络接口的信息 ([RFC 2863](overview-of-ndis-network-interfaces.md))。

NDIS 接口提供程序必须支持这些 Oid。 在本部分中，不是已注册的接口提供程序的驱动程序应支持 Oid。

NDIS 调用[ProviderQueryObject](https://msdn.microsoft.com/library/windows/hardware/ff570399)函数来从接口提供程序发出查询请求的信息。 *ObjectId*此函数的参数包含的对象标识符。 接口提供程序注册*ProviderQueryObject*调用时[NdisIfRegisterProvider](https://msdn.microsoft.com/library/windows/hardware/ff562716)函数注册为接口提供程序。

在句柄*ProviderIfContext*的参数*ProviderQueryObject*函数标识的网络接口。 接口提供程序中调用时，此句柄已提供到 NDIS [NdisIfRegisterInterface](https://msdn.microsoft.com/library/windows/hardware/ff562715)函数来注册接口。 *POutputBuffer*的参数*ProviderQueryObject*函数包含 OID 请求的结果。

网络接口 Oid 的 NDIS 有关的详细信息，请参阅[NDIS 6.0 网络接口](ndis-network-interfaces2.md)。

本部分介绍以下的 NDIS 网络接口 Oid:

- [OID_GEN_ALIAS](https://msdn.microsoft.com/library/windows/hardware/ff569438) 
- [OID_GEN_ADMIN_STATUS](https://msdn.microsoft.com/library/windows/hardware/ff569437) 
- [OID_GEN_OPERATIONAL_STATUS](https://msdn.microsoft.com/library/windows/hardware/ff569619) 
- [OID_GEN_PROMISCUOUS_MODE](https://msdn.microsoft.com/library/windows/hardware/ff569625) 
- [OID_GEN_XMIT_LINK_SPEED](https://msdn.microsoft.com/library/windows/hardware/ff569655) 
- [OID_GEN_RCV_LINK_SPEED](https://msdn.microsoft.com/library/windows/hardware/ff569630) 
- [OID_GEN_UNKNOWN_PROTOS](https://msdn.microsoft.com/library/windows/hardware/ff569648) 
- [OID_GEN_DISCONTINUITY_TIME](https://msdn.microsoft.com/library/windows/hardware/ff569581) 
- [OID_GEN_LAST_CHANGE](https://msdn.microsoft.com/library/windows/hardware/ff569591) 
- [OID_GEN_INTERFACE_INFO](https://msdn.microsoft.com/library/windows/hardware/ff569589) 
- [OID_GEN_MEDIA_CONNECT_STATUS_EX](https://msdn.microsoft.com/library/windows/hardware/ff569605) 
- [OID_GEN_LINK_SPEED_EX](https://msdn.microsoft.com/library/windows/hardware/ff569594) 
- [OID_GEN_MEDIA_DUPLEX_STATE](https://msdn.microsoft.com/library/windows/hardware/ff569606) 
- [OID_TUNNEL_INTERFACE_RELEASE_OID](https://msdn.microsoft.com/library/windows/hardware/dn155803) 
- [OID_TUNNEL_INTERFACE_SET_OID](https://msdn.microsoft.com/library/windows/hardware/dn155804) 



---
title: NDIS 端口 OID 请求
description: NDIS 端口 OID 请求
ms.assetid: 361f9adf-2bf6-4aa8-b66b-fe9304b14550
keywords:
- 端口 WDK NDIS OID 请求
- NDIS 端口 WDK，OID 请求
- OID 请求 WDK NDIS 端口
- 将关联 OID 请求 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e5ffeb2846784540f5d5ff2fd70be73e6b0d68a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354960"
---
# <a name="ndis-port-oid-requests"></a>NDIS 端口 OID 请求





NDIS 驱动程序可以将与 NDIS 端口关联 OID 请求。 在此类 OID 请求中， **PortNumber**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构设置为目标端口号。 OID 请求是否为默认端口，端口号将为零。 基础驱动程序必须确保在任何指定特定的端口号的 OID 请求之前端口处于活动状态。

当调用 NDIS [ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)协议驱动程序，NDIS 函数提供了一系列中的所有当前活动端口**ActivePorts** 的成员[**NDIS\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)结构*BindParameters*参数指向。 NDIS 还会通知与即插即用事件时端口是激活和停用协议驱动程序。 有关即插即用端口的激活和停用通知的详细信息，请参阅[处理 NDIS 端口即插即用通知](handling-ndis-ports-pnp-event-notifications.md)。

以下 Oid 是特定于 NDIS 端口接口：

<a href="" id="oid-gen-enumerate-ports"></a>[OID\_GEN\_ENUMERATE\_端口](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-enumerate-ports)  
枚举活动与微型端口适配器关联的端口。

<a href="" id="oid-gen-port-state"></a>[OID\_GEN\_端口\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-state)  
检索当前的链接和身份验证端口状态。

<a href="" id="--------oid-gen-port-authentication-parameters"></a>[OID\_GEN\_端口\_身份验证\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-authentication-parameters)  
设置 NDIS 端口的当前身份验证状态。

本部分包括：

-   [枚举端口](enumerating-ports.md)
-   [查询端口状态](querying-the-port-state.md)
-   [设置端口身份验证参数](setting-port-authentication-parameters.md)

 

 






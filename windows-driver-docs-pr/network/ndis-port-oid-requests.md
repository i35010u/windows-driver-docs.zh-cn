---
title: NDIS 端口 OID 请求
description: NDIS 端口 OID 请求
ms.assetid: 361f9adf-2bf6-4aa8-b66b-fe9304b14550
keywords:
- 端口 WDK NDIS，OID 请求
- NDIS 端口 WDK，OID 请求
- OID 请求 WDK NDIS 端口
- 关联 OID 请求 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07d5c760c69fc9512fd1740f4bb1f76e850a8e26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826955"
---
# <a name="ndis-port-oid-requests"></a>NDIS 端口 OID 请求





NDIS 驱动程序可以将 OID 请求与 NDIS 端口关联起来。 在此类 OID 请求中， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**PortNumber**成员设置为目标端口号。 如果 OID 请求用于默认端口，则端口号为零。 完成指定特定端口号的任何 OID 请求之前，过量驱动程序必须确保端口处于活动状态。

当 NDIS 调用协议驱动程序的[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数时，Ndis 在[**ndis\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构的 *ActivePorts 成员中提供了所有当前处于活动状态的端口的列表，BindParameters*参数指向。 激活和停用端口时，NDIS 还会通知协议驱动程序具有 PnP 事件。 有关 PnP 端口激活和停用通知的详细信息，请参阅[处理 NDIS 端口 PnP 通知](handling-ndis-ports-pnp-event-notifications.md)。

以下 Oid 特定于 NDIS 端口接口：

<a href="" id="oid-gen-enumerate-ports"></a>[OID\_代\_枚举\_端口](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-enumerate-ports)  
枚举与微型端口适配器关联的活动端口。

<a href="" id="oid-gen-port-state"></a>[OID\_GEN\_端口\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-state)  
检索当前链接和身份验证端口状态。

<a href="" id="--------oid-gen-port-authentication-parameters"></a>[OID\_代\_端口\_AUTHENTICATION\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-authentication-parameters)  
设置 NDIS 端口的当前身份验证状态。

本部分包括：

-   [枚举端口](enumerating-ports.md)
-   [查询端口状态](querying-the-port-state.md)
-   [设置端口身份验证参数](setting-port-authentication-parameters.md)

 

 






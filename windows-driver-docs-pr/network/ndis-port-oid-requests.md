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
ms.openlocfilehash: 2094b4e9744286d3256fcfa41a2617a79ac93b31
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378288"
---
# <a name="ndis-port-oid-requests"></a>NDIS 端口 OID 请求





NDIS 驱动程序可以将与 NDIS 端口关联 OID 请求。 在此类 OID 请求中， **PortNumber**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构设置为目标端口号。 OID 请求是否为默认端口，端口号将为零。 基础驱动程序必须确保在任何指定特定的端口号的 OID 请求之前端口处于活动状态。

当调用 NDIS [ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)协议驱动程序，NDIS 函数提供了一系列中的所有当前活动端口**ActivePorts** 的成员[**NDIS\_绑定\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff564832)结构*BindParameters*参数指向。 NDIS 还会通知与即插即用事件时端口是激活和停用协议驱动程序。 有关即插即用端口的激活和停用通知的详细信息，请参阅[处理 NDIS 端口即插即用通知](handling-ndis-ports-pnp-event-notifications.md)。

以下 Oid 是特定于 NDIS 端口接口：

<a href="" id="oid-gen-enumerate-ports"></a>[OID\_GEN\_ENUMERATE\_端口](https://msdn.microsoft.com/library/windows/hardware/ff569583)  
枚举活动与微型端口适配器关联的端口。

<a href="" id="oid-gen-port-state"></a>[OID\_GEN\_端口\_状态](https://msdn.microsoft.com/library/windows/hardware/ff569624)  
检索当前的链接和身份验证端口状态。

<a href="" id="--------oid-gen-port-authentication-parameters"></a>[OID\_GEN\_端口\_身份验证\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569623)  
设置 NDIS 端口的当前身份验证状态。

本部分包括：

-   [枚举端口](enumerating-ports.md)
-   [查询端口状态](querying-the-port-state.md)
-   [设置端口身份验证参数](setting-port-authentication-parameters.md)

 

 






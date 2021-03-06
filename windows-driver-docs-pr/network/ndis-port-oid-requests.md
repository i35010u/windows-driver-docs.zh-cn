---
title: NDIS 端口 OID 请求
description: NDIS 端口 OID 请求
keywords:
- 端口 WDK NDIS，OID 请求
- NDIS 端口 WDK，OID 请求
- OID 请求 WDK NDIS 端口
- 关联 OID 请求 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f3705dff16e061b948d6d1b2eabc2b475a8cc3b
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248445"
---
# <a name="ndis-port-oid-requests"></a>NDIS 端口 OID 请求





NDIS 驱动程序可以将 OID 请求与 NDIS 端口关联起来。 在此类 OID 请求中， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **PortNumber** 成员设置为目标端口号。 如果 OID 请求用于默认端口，则端口号为零。 完成指定特定端口号的任何 OID 请求之前，过量驱动程序必须确保端口处于活动状态。

当 NDIS 调用协议驱动程序的 [*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数时，ndis 会提供 *BindParameters* 参数指向的 [**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构的 **ActivePorts** 成员中所有当前活动端口的列表。 激活和停用端口时，NDIS 还会通知协议驱动程序具有 PnP 事件。 有关 PnP 端口激活和停用通知的详细信息，请参阅 [处理 NDIS 端口 PnP 通知](handling-ndis-ports-pnp-event-notifications.md)。

以下 Oid 特定于 NDIS 端口接口：

<a href="" id="oid-gen-enumerate-ports"></a>[OID \_ 代 \_ 枚举 \_ 端口](./oid-gen-enumerate-ports.md)  
枚举与微型端口适配器关联的活动端口。

<a href="" id="oid-gen-port-state"></a>[OID \_ 生成 \_ 端口 \_ 状态](./oid-gen-port-state.md)  
检索当前链接和身份验证端口状态。

<a href="" id="--------oid-gen-port-authentication-parameters"></a>[OID \_ GEN \_ 端口 \_ 身份验证 \_ 参数](./oid-gen-port-authentication-parameters.md)  
设置 NDIS 端口的当前身份验证状态。

本节包括：

-   [枚举端口](enumerating-ports.md)
-   [查询端口状态](querying-the-port-state.md)
-   [设置端口身份验证参数](setting-port-authentication-parameters.md)

 


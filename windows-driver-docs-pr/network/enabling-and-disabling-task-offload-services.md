---
title: 启用和禁用任务卸载服务
description: 协议驱动程序可以通过发出 OID_OFFLOAD_ENCAPSULATION OID 设置请求，启用或禁用基础微型端口适配器的任务卸载服务。
keywords:
- 任务卸载 WDK TCP/IP 传输，启用服务
- 任务卸载 WDK TCP/IP 传输，禁用服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59e11da7757ad3dae35267e8c8fc9544fc45435e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822955"
---
# <a name="enabling-and-disabling-task-offload-services"></a>启用和禁用任务卸载服务


协议驱动程序可以通过发出 [oid \_ 卸载 \_ 封装](./oid-offload-encapsulation.md) oid 设置请求，启用或禁用底层微型端口适配器的任务卸载服务。 此 OID 请求设置所需的封装类型，并告知微型端口驱动程序激活所有可用的任务卸载服务。




在发出 [oid \_ 卸载 \_ 封装](./oid-offload-encapsulation.md) OID set 请求之前，协议驱动程序应确保基础微型端口适配器支持所需的封装类型。 有两种方法可以实现此目的：

-   检查协议驱动程序在其 [*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数中收到的 [**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构。
-   发出 [OID \_ TCP \_ 卸载当前的 \_ \_ 配置](./oid-tcp-offload-current-config.md) 查询请求。

如果微型端口驱动程序支持任何支持请求的封装类型的任务卸载类型，微型端口驱动程序必须返回 NDIS \_ 状态 \_ "成功" 以响应 [OID \_ 卸载 \_ 封装](./oid-offload-encapsulation.md) 集请求。 否则，微型端口驱动程序应返回 NDIS \_ 状态 \_ 无效 \_ 参数。

 


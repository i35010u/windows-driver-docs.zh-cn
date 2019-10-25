---
title: 启用和禁用任务卸载服务
description: 协议驱动程序可以通过发出 OID_OFFLOAD_ENCAPSULATION OID 集请求来启用或禁用基础微型端口适配器的任务卸载服务。
ms.assetid: cc803af4-d4ed-4b51-9e0e-77443e0eb023
keywords:
- 任务卸载 WDK TCP/IP 传输，启用服务
- 任务卸载 WDK TCP/IP 传输，禁用服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18f6e9c3a95a49e51f4963f6cfb7748f6e255dc1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834782"
---
# <a name="enabling-and-disabling-task-offload-services"></a>启用和禁用任务卸载服务


协议驱动程序可以通过发出[oid\_卸载\_封装](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)oid 集请求来为基础微型端口适配器启用或禁用任务卸载服务。 此 OID 请求设置所需的封装类型，并告知微型端口驱动程序激活所有可用的任务卸载服务。




在发出[oid\_卸载\_封装](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)OID 集请求之前，协议驱动程序应确保基础微型端口适配器支持所需的封装类型。 可以通过两种方法执行此操作：

-   检查[**NDIS\_绑定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)协议驱动程序在其[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数中收到的\_参数结构。
-   发出[OID\_TCP\_卸载\_当前\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)查询请求。

如果微型端口驱动程序支持任何支持请求的封装类型的任务卸载类型，微型端口驱动程序必须返回 NDIS\_\_状态，以响应[OID\_卸载\_封装](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)集请求。 否则，微型端口驱动程序应返回 NDIS\_状态\_无效\_参数。

 

 






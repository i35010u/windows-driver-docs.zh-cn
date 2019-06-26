---
title: 启用和禁用任务卸载服务
description: 协议驱动程序可以启用或禁用任务卸载服务为基础的微型端口适配器通过发出 OID_OFFLOAD_ENCAPSULATION OID 集请求。
ms.assetid: cc803af4-d4ed-4b51-9e0e-77443e0eb023
keywords:
- 任务卸载，WDK TCP/IP 传输，启用服务
- 任务卸载，WDK TCP/IP 传输，禁用服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 145dc26a97c63d610962c76aed3059fdb7c9ff84
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378693"
---
# <a name="enabling-and-disabling-task-offload-services"></a>启用和禁用任务卸载服务


协议驱动程序可以启用或禁用任务卸载服务为基础的微型端口适配器通过发出[OID\_卸载\_封装](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)OID 设置请求。 此 OID 请求所需的封装类型设置，并指示微型端口驱动程序激活的所有可用的任务卸载服务。




发出之前[OID\_卸载\_封装](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)OID 设置请求，协议驱动程序应确保基础的微型端口适配器支持所需的封装类型。 有两种方法来执行此操作：

-   检查[ **NDIS\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)协议驱动程序中收到的结构及其[ *ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)函数。
-   问题[OID\_TCP\_卸载\_当前\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)查询请求。

微型端口驱动程序微型端口驱动程序支持任何支持请求的封装类型的任务卸载类型，如果必须返回 NDIS\_状态\_成功响应[OID\_卸载\_封装](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)集请求。 否则，微型端口驱动程序应返回 NDIS\_状态\_无效\_参数。

 

 






---
title: 启用和禁用任务卸载服务
description: 协议驱动程序可以启用或禁用任务卸载服务为基础的微型端口适配器通过发出 OID_OFFLOAD_ENCAPSULATION OID 集请求。
ms.assetid: cc803af4-d4ed-4b51-9e0e-77443e0eb023
keywords:
- 任务卸载，WDK TCP/IP 传输，启用服务
- 任务卸载，WDK TCP/IP 传输，禁用服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 294d006b596b21477c817c60b6c957a7dd6ee8c1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372502"
---
# <a name="enabling-and-disabling-task-offload-services"></a>启用和禁用任务卸载服务


协议驱动程序可以启用或禁用任务卸载服务为基础的微型端口适配器通过发出[OID\_卸载\_封装](https://msdn.microsoft.com/library/windows/hardware/ff569762)OID 设置请求。 此 OID 请求所需的封装类型设置，并指示微型端口驱动程序激活的所有可用的任务卸载服务。




发出之前[OID\_卸载\_封装](https://msdn.microsoft.com/library/windows/hardware/ff569762)OID 设置请求，协议驱动程序应确保基础的微型端口适配器支持所需的封装类型。 有两种方法来执行此操作：

-   检查[ **NDIS\_绑定\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff564832)协议驱动程序中收到的结构及其[ *ProtocolBindAdapterEx*](https://msdn.microsoft.com/library/windows/hardware/ff570220)函数。
-   问题[OID\_TCP\_卸载\_当前\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569805)查询请求。

微型端口驱动程序微型端口驱动程序支持任何支持请求的封装类型的任务卸载类型，如果必须返回 NDIS\_状态\_成功响应[OID\_卸载\_封装](https://msdn.microsoft.com/library/windows/hardware/ff569762)集请求。 否则，微型端口驱动程序应返回 NDIS\_状态\_无效\_参数。

 

 






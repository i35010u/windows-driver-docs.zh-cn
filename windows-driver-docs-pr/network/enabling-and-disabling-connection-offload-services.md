---
title: 启用和禁用连接卸载服务
description: 启用和禁用连接卸载服务
ms.assetid: 3d353f87-1cd7-483a-b8eb-d45ec3b8f94e
keywords:
- 连接将卸载 WDK TCP/IP 传输，启用服务
- 连接将卸载 WDK TCP/IP 传输，禁用服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c031940bf2ea35467aebf7ec82684bd31fea0faa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378690"
---
# <a name="enabling-and-disabling-connection-offload-services"></a>启用和禁用连接卸载服务





协议驱动程序启用连接卸载服务使用的对象标识符 (OID) 请求。

**请注意**  启用或禁用任务卸载服务是不同于启用或禁用连接卸载服务。 协议驱动程序指定封装类型后，微型端口驱动程序将激活的所有可用的任务卸载服务。

 

TCP/IP 传输启用或禁用网络接口卡 (NIC) 的连接卸载功能，通过设置[OID\_TCP\_连接\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-parameters)OID。 在此设置操作，TCP/IP 传输将传递 NDIS\_TCP\_连接\_卸载\_参数结构**InformationBuffer** 成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构。 (有关信息 NDIS\_TCP\_连接\_卸载\_参数，请参阅[NDIS 6.0 TCP 烟囱卸载文档](full-tcp-offload.md)。)

有关配置连接的详细信息将卸载服务，请参阅初始化中卸载的目标[NDIS 6.0 TCP 烟囱卸载文档](full-tcp-offload.md)。

 

 






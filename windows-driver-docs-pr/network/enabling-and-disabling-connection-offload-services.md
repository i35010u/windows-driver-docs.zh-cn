---
title: 启用和禁用连接卸载服务
description: 启用和禁用连接卸载服务
ms.assetid: 3d353f87-1cd7-483a-b8eb-d45ec3b8f94e
keywords:
- 连接卸载 WDK TCP/IP 传输，启用服务
- 连接卸载 WDK TCP/IP 传输，禁用服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21e76b8c4ef870379e0e4af186e773d872ea4e66
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838126"
---
# <a name="enabling-and-disabling-connection-offload-services"></a>启用和禁用连接卸载服务





协议驱动程序通过对象标识符（OID）请求启用连接卸载服务。

**请注意**  启用或禁用任务卸载服务不同于启用或禁用连接卸载服务。 小型端口驱动程序在协议驱动程序指定封装类型后激活所有可用的任务卸载服务。

 

TCP/IP 传输通过设置[\_TCP\_连接\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-parameters)OID，启用或禁用网络接口卡（NIC）的连接卸载功能。 在此设置操作中，TCP/IP 传输将 NDIS\_TCP\_连接\_卸载\_参数结构（在[**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员中）。 （有关 NDIS\_TCP\_连接\_卸载\_参数的信息，请参阅[ndis 6.0 tcp 烟囱卸载文档](full-tcp-offload.md)。）

有关配置连接卸载服务的详细信息，请参阅[NDIS 6.0 TCP 烟囱卸载文档](full-tcp-offload.md)中的初始化卸载目标。

 

 






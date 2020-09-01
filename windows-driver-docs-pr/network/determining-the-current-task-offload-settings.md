---
title: 确定当前任务卸载设置
description: 本部分介绍如何确定协议驱动程序的当前任务卸载设置
ms.assetid: cd2f9b9f-f455-405d-8775-9a437e628476
keywords:
- 任务卸载 WDK TCP/IP 传输，当前设置
- 当前任务加载设置 WDK TCP/IP 卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea2beeea5bb2b7cfee5e1e7052b342fa7dd12642
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212525"
---
# <a name="determining-the-current-task-offload-settings"></a>确定当前的任务卸载设置


协议驱动程序可以通过发出 [oid \_ 卸载 \_ 封装](./oid-offload-encapsulation.md) OID 查询请求来确定基础微型端口适配器的当前任务卸载封装设置。




有关发出 OID 请求的详细信息，请参阅 [从 NDIS 协议驱动程序生成 OID 请求](generating-oid-requests-from-an-ndis-protocol-driver.md)。

 


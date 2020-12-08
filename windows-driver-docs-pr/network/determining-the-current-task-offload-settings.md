---
title: 确定当前任务卸载设置
description: 本部分介绍如何确定协议驱动程序的当前任务卸载设置
keywords:
- 任务卸载 WDK TCP/IP 传输，当前设置
- 当前任务加载设置 WDK TCP/IP 卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8eae9487e9cf84c8c605b39d4fc44ae39432fa7f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817593"
---
# <a name="determining-the-current-task-offload-settings"></a>确定当前的任务卸载设置


协议驱动程序可以通过发出 [oid \_ 卸载 \_ 封装](./oid-offload-encapsulation.md) OID 查询请求来确定基础微型端口适配器的当前任务卸载封装设置。




有关发出 OID 请求的详细信息，请参阅 [从 NDIS 协议驱动程序生成 OID 请求](generating-oid-requests-from-an-ndis-protocol-driver.md)。

 


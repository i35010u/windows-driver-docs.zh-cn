---
title: 接收端缩放支持
description: 接收端缩放支持
ms.assetid: db0d8178-ae6c-4513-9c8c-f10615d1bbce
keywords:
- 可伸缩网络 WDK
- 接收方缩放 WDK 网络
- RSS WDK 网络
- 微型端口驱动程序 WDK 网络，缩放接收数据包处理
- NDIS 微型端口驱动程序 WDK，缩放接收数据包处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa3232a3b070d805e25e8f4396122b9d8606f49b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209625"
---
# <a name="receive-side-scaling-support"></a>接收端缩放支持





NDIS 6.0 引入了对跨多个处理器的接收数据包处理的扩展的支持。 接收方缩放 (RSS) 接口提供多个 NIC 硬件支持级别。

根据其当前 RSS 配置，微型端口驱动程序或 NIC 确定要与接收的数据关联的目标处理器。 可以调整 RSS 配置以充分利用可用目标处理器。

微型端口驱动程序或 NIC 将接收的数据分配给与目标处理器关联的接收队列。 微型端口驱动程序请求 NDIS 为包含非空接收队列 (Dpc) 计划延迟的过程调用。

NDIS 计划每个指定目标处理器上的一个 DPC。 每个 DPC 处理指定目标处理器上的特定接收队列。

有关 NDIS 6.0 接收方缩放的详细信息，请参阅 [接收方缩放](./receive-side-scaling-version-2-rssv2-.md)。

 


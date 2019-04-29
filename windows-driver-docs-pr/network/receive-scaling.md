---
title: 接收端缩放支持
description: 接收端缩放支持
ms.assetid: db0d8178-ae6c-4513-9c8c-f10615d1bbce
keywords:
- 可缩放网络 WDK
- 接收方缩放 WDK 网络
- RSS WDK 网络
- 缩放接收数据包处理的微型端口驱动程序 WDK 网络
- NDIS 微型端口驱动程序 WDK，缩放接收数据包处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7dfbc32f26760f9febe475b0ecd52067a122e9b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372218"
---
# <a name="receive-side-scaling-support"></a>接收端缩放支持





NDIS 6.0 引入了对接收数据包处理跨多个处理器的缩放支持。 接收方缩放 (RSS) 接口可容纳多个级别的 NIC 硬件支持。

根据其当前的 RSS 配置，微型端口驱动程序或 NIC 确定目标处理器能够接收到的数据相关联。 RSS 配置可以进行调整，以最有效利用可用的目标处理器。

微型端口驱动程序或 NIC 分配到与目标处理器关联的接收队列接收到的数据。 计划具有非空的目标处理器的延缓的过程调用 (Dpc) 的微型端口驱动程序请求 NDIS 接收队列。

NDIS 计划在每个指定的目标处理器上 DPC。 每个 DPC 处理指定的目标处理器上的特定接收队列。

详细了解 NDIS 6.0 接收方缩放，请参阅[接收方伸缩](ndis-receive-side-scaling2.md)。

 

 






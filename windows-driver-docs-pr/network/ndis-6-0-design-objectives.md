---
title: NDIS 6.0 设计目标
description: NDIS 6.0 设计目标
ms.assetid: 1b59bc97-be79-47ba-8e39-208a9d38f6b9
keywords:
- NDIS WDK，有关 NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dccf5382b1a2308ac2843dcb626e41275dc5fb7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525449"
---
# <a name="ndis-60-design-objectives"></a>NDIS 6.0 设计目标





设计和开发的 NDIS 6.0 具有按两个主要目标：

1.  增强的驱动程序性能和可伸缩性。 (请参阅[增强的性能和可伸缩性](enhanced-performance-and-scalability.md)有关详细信息。)

    以下重大改进客户端和服务器提供显著的性能提升：

    -   网络数据打包
    -   发送和接收路径
    -   运行时重新配置功能
    -   散播-聚集 DMA
    -   筛选器驱动程序
    -   接收到的数据处理的多处理器缩放
    -   卸载到 Nic 的 TCP 任务

2.  简化的 NDIS 驱动程序模型。 (请参阅[简化驱动程序模型](simplified-driver-model.md)有关详细信息。)

    以下改进简化驱动程序开发：

    -   简化驱动程序初始化
    -   NDIS 接口的版本控制支持
    -   简化重置处理
    -   标准接口，用于获取管理信息
    -   要将筛选器中间驱动程序的筛选器驱动程序模型

 

 






---
title: NDIS 6.0 设计目标
description: NDIS 6.0 设计目标
keywords:
- NDIS WDK，关于 NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c450c397e3165238b4bd25346aa4fc7a88f295db
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815935"
---
# <a name="ndis-60-design-objectives"></a>NDIS 6.0 设计目标





两个主要目标已经指导您设计和开发 NDIS 6.0：

1.  增强驱动程序的性能和可伸缩性。 有关详细信息，请参阅 [增强的性能和可伸缩性](enhanced-performance-and-scalability.md) (。 ) 

    下面的重大改进为客户端和服务器提供了显著的性能提升：

    -   网络数据打包
    -   发送和接收路径
    -   运行时重新配置功能
    -   散点/集合 DMA
    -   筛选器驱动程序
    -   接收的数据处理的多处理器缩放
    -   将 TCP 任务卸载到 Nic

2.  简化 NDIS 驱动程序模型。 有关详细信息，请参阅 [简化的驱动程序型号](simplified-driver-model.md) (。 ) 

    以下改进简化了驱动程序的开发：

    -   简化的驱动程序初始化
    -   对 NDIS 接口的版本控制支持
    -   简化的重置处理
    -   用于获取管理信息的标准接口
    -   用于替换筛选器中间驱动程序的筛选器驱动程序模型

 

 






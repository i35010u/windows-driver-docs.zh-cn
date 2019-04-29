---
title: NDIS MSI-X
description: NDIS MSI-X
ms.assetid: 5bb374c8-9354-42d3-9754-42e8ff42bdb9
keywords:
- 微型端口驱动程序 WDK 网络，MSI X
- NDIS 微型端口驱动程序 WDK，MSI X
- MSI X WDK 网络
- 消息信号中断 WDK 网络
- Msi WDK 网络
- 中断 WDK 网络
- 中断关联 WDK 网络
- 中断 WDK net
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8228dcc831573067e11d94bd0c7da2caf54f766a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378354"
---
# <a name="ndis-msi-x"></a>NDIS MSI-X





消息信号中断 (Msi) 提供了传统的基于线条的中断的网络设备和其微型端口驱动程序可以使用一种替代方法。 操作系统从 Windows Vista 开始，支持两种类型的 Msi:PCI V2.2 MSI 和 PCI V3.0 MSI-X。

支持 MSI X 的微型端口驱动程序可以指定*中断关联*，这是驱动程序的消息中断服务例程运行的中央处理单元 (Cpu) 的子集。 您可以指定中断关联的每个 MSI X 消息--例如，可以指定中断计算机上使用非一致性内存访问 (NUMA) 体系结构方面"邻近性"的设备到特定 Cpu 的相关性。

MSI X 支持可以提供显著的性能优势，特别是对于支持接收方缩放 (RSS) 的网络接口卡 (Nic)。 有关详细信息接收方缩放，请参阅[接收方伸缩](ndis-receive-side-scaling2.md)。

有关基于行的中断的详细信息，请参阅[管理中断](managing-interrupts.md)。

本部分包括：

[MSI X 初始化](msi-x-initialization.md)

[处理 MSI 中断](handling-an-msi-interrupt.md)

[与 MSI 中断同步](synchronizing-with-an-msi-interrupt.md)

[更改表项 MSI X CPU 关联](changing-the-cpu-affinity-of-msi-x-table-entries.md)

 

 






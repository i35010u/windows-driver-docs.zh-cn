---
title: NDIS MSI-X 概述
description: NDIS MSI-X 概述
ms.assetid: 5bb374c8-9354-42d3-9754-42e8ff42bdb9
keywords:
- 微型端口驱动程序 WDK 网络, MSI-X
- NDIS 微型端口驱动程序 WDK、MSI-X
- MSI-X WDK 网络
- 消息-已发出信号中断 WDK 网络
- Msi WDK 网络
- 中断 WDK 网络
- 中断关联 WDK 网络
- 中断 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea37bf478cac493a78e5a0fbd1a38b1a9d92c5ef
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565649"
---
# <a name="overview-of-ndis-msi-x"></a>NDIS MSI-X 概述





消息信号中断 (Msi) 提供了一种替代网络设备及其微型端口驱动程序可以使用的传统的基于行的中断。 从 Windows Vista 开始, 操作系统支持两种类型的 Msi:PCI v2.0 MSI 和 PCI 3.0 MSI-X。

支持 MSI X 的微型端口驱动程序可以指定*中断关联*, 这是驱动程序消息中断服务例程在其上运行的中央处理单元 (cpu) 的子集。 你可以为每个 MSI-X 消息指定中断关联-例如, 你可以在具有非一致性内存访问 (NUMA) 体系结构的计算机上, 使用非一致性内存访问 (NUMA) 体系结构在特定 Cpu 上指定中断相关性。

支持接收方缩放 (RSS) 的网络接口卡 (Nic) 尤其适用于支持接收方缩放 (RSS) 的网络接口卡 (Nic), 支持 MSI X 支持。 有关接收方缩放的详细信息, 请参阅[接收方缩放](ndis-receive-side-scaling2.md)。

有关基于行的中断的详细信息, 请参阅[管理中断](managing-interrupts.md)。

本部分包括：

[MSI-X 初始化](msi-x-initialization.md)

[处理 MSI 中断](handling-an-msi-interrupt.md)

[与 MSI 中断同步](synchronizing-with-an-msi-interrupt.md)

[更改 MSI-X 表条目的 CPU 关联](changing-the-cpu-affinity-of-msi-x-table-entries.md)

 

 






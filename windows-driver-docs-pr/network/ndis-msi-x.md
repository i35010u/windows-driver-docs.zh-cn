---
title: NDIS MSI-X 概述
description: NDIS MSI-X 概述
keywords:
- 微型端口驱动程序 WDK 网络，MSI-X
- NDIS 微型端口驱动程序 WDK、MSI-X
- MSI-X WDK 网络
- 消息-已发出信号中断 WDK 网络
- Msi WDK 网络
- 中断 WDK 网络
- 中断关联 WDK 网络
- 中断 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6865f52ffa35e2b1c989eb52806fd0c66507976
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801583"
---
# <a name="overview-of-ndis-msi-x"></a>NDIS MSI-X 概述





 (Msi 的消息信号中断) 提供网络设备及其微型端口驱动程序可以使用的传统的基于行中断的替代方法。 从 Windows Vista 开始，操作系统支持两种类型的 Msi： PCI v2.0 MSI 和 PCI 3.0 MSI-X。

支持 MSI X 的微型端口驱动程序可以指定 *中断关联*，这是在驱动程序的消息中断服务例程 (cpu) 的中央处理单元的子集。 你可以为每个 MSI-X 消息指定中断关联-例如，你可以在具有非一致性内存访问权限的计算机上指定中断相关性， (NUMA) 体系结构，从其设备的 "nearness" 到特定 Cpu。

支持 (RSS) 接收方缩放的网络接口卡 (的 Nic) ，可提供显著的性能优势。 有关接收方缩放的详细信息，请参阅 [接收方缩放](./receive-side-scaling-version-2-rssv2-.md)。

有关基于行的中断的详细信息，请参阅 [管理中断](registering-and-deregistering-interrupts.md)。

本节包括：

[MSI-X 初始化](msi-x-initialization.md)

[处理 MSI 中断](handling-an-msi-interrupt.md)

[与 MSI 中断同步](synchronizing-with-an-msi-interrupt.md)

[更改 MSI-X 表项的 CPU 关联](changing-the-cpu-affinity-of-msi-x-table-entries.md)

 


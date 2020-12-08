---
title: 开始编写 VMQ 驱动程序
description: 本部分提供有关将 NDIS 虚拟机队列写入 (VMQ) 驱动程序的信息。 在阅读本部分之前，您应该已经了解虚拟机队列的体系结构。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 050f352687f53d0ac2bf4df41b233d816a6f2cf6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813629"
---
# <a name="getting-started-writing-vmq-drivers"></a>开始编写 VMQ 驱动程序


本部分提供有关将 NDIS 虚拟机队列写入 (VMQ) 驱动程序的信息。 在阅读本部分之前，您应该已经了解 [虚拟机队列的体系结构](virtual-machine-queue-architecture.md) 。

**注意**  务必研究 [NDIS 虚拟微端口驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617918)，尤其是 vmq 和 vmq 源文件。

支持 VMQ 的微型端口驱动程序可管理提供 VMQ 硬件支持的 Nic。 这种 NIC 提供硬件服务来筛选传入的网络数据，并将其分配给 VM 接收队列。

本部分介绍过量驱动程序如何获取有关基础网络适配器的信息，以及如何设置 VMQ 配置。 过量驱动程序和用户应用程序可以获取当前配置并启用或禁用 VMQ 功能。

本节包括下列主题：

-   [VMQ 驱动程序配置](vmq-driver-configuration.md)
-   [队列状态和操作](queue-states-and-operations.md)
-   [VMQ 中断要求](vmq-interrupt-requirements.md)
-   [分配和释放 VM 队列](allocating-and-freeing-vm-queues.md)
-   [设置和清除 VMQ 筛选器](setting-and-clearing-vmq-filters.md)
-   [获取和更新 VM 队列参数](obtaining-and-updating-vm-queue-parameters.md)
-   [VMQ 发送和接收操作](vmq-send-and-receive-operations.md)
-   [获取 VMQ 信息](obtaining-vmq-information.md)

 

 






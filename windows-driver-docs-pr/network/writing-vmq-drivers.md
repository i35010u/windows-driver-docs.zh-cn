---
title: 编写 VMQ 驱动程序入门
description: 本部分提供有关编写 NDIS 虚拟机队列 (VMQ) 驱动程序的信息。 在阅读本部分之前, 您应该已经了解虚拟机队列的体系结构。
ms.assetid: 877d3d95-2ec5-4d2e-9bcc-cd2adfc2a667
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1a9194ec15d9559d96bdef69b20d750bdb927a5
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565703"
---
# <a name="getting-started-writing-vmq-drivers"></a>编写 VMQ 驱动程序入门


本部分提供有关编写 NDIS 虚拟机队列 (VMQ) 驱动程序的信息。 在阅读本部分之前, 您应该已经了解[虚拟机队列的体系结构](virtual-machine-queue-architecture.md)。

**请注意**  , 请务必学习[NDIS 虚拟微端口驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617918), 尤其是 vmq 和 vmq 源文件。

支持 VMQ 的微型端口驱动程序可管理提供 VMQ 硬件支持的 Nic。 这种 NIC 提供硬件服务来筛选传入的网络数据, 并将其分配给 VM 接收队列。

本部分介绍过量驱动程序如何获取有关基础网络适配器的信息, 以及如何设置 VMQ 配置。 过量驱动程序和用户应用程序可以获取当前配置并启用或禁用 VMQ 功能。

本部分包括以下主题：

-   [VMQ 驱动程序配置](vmq-driver-configuration.md)
-   [队列状态和操作](queue-states-and-operations.md)
-   [VMQ 中断要求](vmq-interrupt-requirements.md)
-   [分配和释放 VM 队列](allocating-and-freeing-vm-queues.md)
-   [设置和清除 VMQ 筛选器](setting-and-clearing-vmq-filters.md)
-   [获取和更新 VM 队列参数](obtaining-and-updating-vm-queue-parameters.md)
-   [VMQ 发送和接收操作](vmq-send-and-receive-operations.md)
-   [获取 VMQ 信息](obtaining-vmq-information.md)

 

 






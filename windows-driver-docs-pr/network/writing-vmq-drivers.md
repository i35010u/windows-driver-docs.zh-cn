---
title: 编写 VMQ 驱动程序
description: 本部分提供有关编写 NDIS 虚拟机队列 (VMQ) 驱动程序的信息。 您应已了解之前阅读此部分的虚拟机队列体系结构。
ms.assetid: 877d3d95-2ec5-4d2e-9bcc-cd2adfc2a667
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e5dae3e783613f339f2f1ac3f97b6bbb2dd2941
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340914"
---
# <a name="writing-vmq-drivers"></a>编写 VMQ 驱动程序


本部分提供有关编写 NDIS 虚拟机队列 (VMQ) 驱动程序的信息。 您应该已经了解[虚拟机队列体系结构](virtual-machine-queue-architecture.md)阅读本节之前。

**请注意**  务必研究[NDIS 虚拟微型端口驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617918)，尤其是 vmq.c 和 vmq.h 源文件。

 




支持 VMQ 的微型端口驱动程序管理提供 VMQ 硬件支持的 Nic。 此类 NIC 提供硬件服务来筛选传入的网络数据，并将其分配给 VM 接收队列。

本部分介绍如何过量驱动程序获取有关基础的网络适配器的信息和设置 VMQ 配置。 过量驱动程序和用户应用程序可以获取当前配置并启用或禁用 VMQ 功能。

本部分包括以下主题：

-   [VMQ 驱动程序配置](vmq-driver-configuration.md)
-   [队列状态和操作](queue-states-and-operations.md)
-   [VMQ 中断要求](vmq-interrupt-requirements.md)
-   [分配和释放虚拟机队列](allocating-and-freeing-vm-queues.md)
-   [设置和清除 VMQ 筛选器](setting-and-clearing-vmq-filters.md)
-   [获取和更新虚拟机队列参数](obtaining-and-updating-vm-queue-parameters.md)
-   [VMQ 发送和接收操作](vmq-send-and-receive-operations.md)
-   [获取 VMQ 信息](obtaining-vmq-information.md)

 

 






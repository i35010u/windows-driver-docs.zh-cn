---
title: Hyper-V 可扩展交换机保存和还原操作
description: Hyper-V 可扩展交换机保存和还原操作
ms.assetid: 7F3A77E0-F1E9-49E4-8C78-62B8F412353D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7743172210dd2e67569ed6b2a6c0c3495b3a5f61
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349513"
---
# <a name="hyper-v-extensible-switch-save-and-restore-operations"></a>Hyper-V 可扩展交换机保存和还原操作


当 HYPER-V 子分区已停止、 已保存，或实时迁移时，保存该分区的运行时状态。 当分区重新启动或已完成实时迁移到另一台主机计算机时，还原的运行时状态。 在保存和还原状态之间转换，期间子分区的网络接口的设置不变，并到 HYPER-V 可扩展交换机的网络连接不销毁。

可扩展交换机接口通知的保存的基础扩展和子分区的还原操作。 在保存操作，该扩展可以返回每个可扩展交换机的网络适配器 (NIC) 的运行时数据。 在还原操作时，接口将运行时数据返回到该扩展，以便它可以还原状态的 nic。

本部分包括以下主题：

[保存操作的 HYPER-V 可扩展交换机](hyper-v-extensible-switch-save-operations.md)

[HYPER-V 可扩展交换机还原操作](hyper-v-extensible-switch-restore-operations.md)

[HYPER-V 可扩展交换机实时迁移支持](hyper-v-extensible-switch-live-migration-support.md)

 

 






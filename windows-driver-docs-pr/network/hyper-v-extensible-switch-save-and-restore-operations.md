---
title: Hyper-v 可扩展交换机保存和还原操作概述
description: Hyper-v 可扩展交换机保存和还原操作概述
ms.assetid: 7F3A77E0-F1E9-49E4-8C78-62B8F412353D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dec3f95a638c7173dba3fb550e641729a3713bb7
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565668"
---
# <a name="hyper-v-extensible-switch-save-and-restore-operations-overview"></a>Hyper-v 可扩展交换机保存和还原操作概述


当 Hyper-v 子分区停止、保存或实时迁移时, 将保存该分区的运行时状态。 当重新启动分区或已完成将实时迁移到另一台主机时, 将还原运行时状态。 在已保存和已还原状态之间过渡期间, 子分区的网络接口的设置不变, 并且与 Hyper-v 可扩展交换机之间的网络连接不会被破坏。

可扩展交换机接口通知子分区保存和还原操作的基础扩展。 在保存操作期间, 扩展可以返回每个可扩展交换机网络适配器 (NIC) 的运行时数据。 在还原操作过程中, 接口会将运行时数据返回到扩展, 以便它可以还原 NIC 的状态。

本部分包括以下主题：

[Hyper-v 可扩展交换机保存操作](hyper-v-extensible-switch-save-operations.md)

[Hyper-v 可扩展交换机还原操作](hyper-v-extensible-switch-restore-operations.md)

[Hyper-v 可扩展交换机实时迁移支持](hyper-v-extensible-switch-live-migration-support.md)

 

 






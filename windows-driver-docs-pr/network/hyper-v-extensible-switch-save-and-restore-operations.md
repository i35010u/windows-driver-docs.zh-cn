---
title: Hyper-V 可扩展交换机保存和还原操作概述
description: Hyper-V 可扩展交换机保存和还原操作概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6af8e3c9a9ab3fea0403f136a27d12ebb63bf819
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828469"
---
# <a name="hyper-v-extensible-switch-save-and-restore-operations-overview"></a>Hyper-V 可扩展交换机保存和还原操作概述


当 Hyper-v 子分区停止、保存或实时迁移时，将保存该分区的运行时状态。 当重新启动分区或已完成将实时迁移到另一台主机时，将还原运行时状态。 在已保存和已还原状态之间过渡期间，子分区的网络接口的设置不变，并且与 Hyper-v 可扩展交换机之间的网络连接不会被破坏。

可扩展交换机接口通知子分区保存和还原操作的基础扩展。 在保存操作期间，扩展可以返回每个可扩展交换机网络适配器的运行时数据 (NIC) 。 在还原操作过程中，接口会将运行时数据返回到扩展，以便它可以还原 NIC 的状态。

本节包括下列主题：

[Hyper-V 可扩展交换机保存操作](hyper-v-extensible-switch-save-operations.md)

[Hyper-V 可扩展交换机还原操作](hyper-v-extensible-switch-restore-operations.md)

[Hyper-V 可扩展交换机实时迁移支持](hyper-v-extensible-switch-live-migration-support.md)

 

 






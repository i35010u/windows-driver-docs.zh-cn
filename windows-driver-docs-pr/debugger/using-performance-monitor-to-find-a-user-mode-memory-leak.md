---
title: 使用性能监视器查找用户模式内存泄漏
description: 使用性能监视器查找用户模式内存泄漏
ms.assetid: 07ba4c55-299c-4558-b4c7-4ffe5c47f496
keywords:
- 内存泄漏, 用户模式, 性能监视器
ms.date: 05/23/2017
ms.localizationpriority: high
ms.openlocfilehash: 37a669e3f196ef32ea40bafd15fa526f44080715
ms.sourcegitcommit: 29d9e97439f19d2c5a090006640e4e5659e56412
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2020
ms.locfileid: "78335951"
---
# <a name="using-performance-monitor-to-find-a-user-mode-memory-leak"></a>使用性能监视器查找用户模式内存泄漏


如果怀疑用户模式存在内存泄漏，但不确定是哪个进程导致了这种情况，则可以使用性能监视器来测量各个进程的内存使用情况。

启动性能监视器。 添加以下计数器：

-   “进程”  --&gt;“专用字节”  （针对要检查的每个进程）

-   “进程”  --&gt;“虚拟字节”  （针对要检查的每个进程）

将更新时间更改为 600 秒，捕获一段时间内的泄漏分析图。 你可能还想要将数据记录到文件中，以供以后检查。

专用字节计数器指示进程已分配的内存总量，不包括与其他进程共享的内存量  。 虚拟字节计数器指示进程正在使用的虚拟地址空间的当前大小  。

当分配的专用字节增加时，数据文件中会出现一些内存泄漏。 当虚拟地址空间增加时，会出现其他内存泄漏。

确定正在泄漏内存的进程之后，请使用 UMDH 工具确定出错的特定例程。 有关详细信息，请参阅[使用 UMDH 查找用户模式内存泄漏](using-umdh-to-find-a-user-mode-memory-leak.md)。

 

 






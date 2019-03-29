---
title: 使用性能监视器查找用户模式内存泄漏
description: 使用性能监视器查找用户模式内存泄漏
ms.assetid: 07ba4c55-299c-4558-b4c7-4ffe5c47f496
keywords:
- 内存泄漏，用户模式下，性能监视器
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 801c4054641a86c6fab32a334dc58b8f89d555df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576101"
---
# <a name="using-performance-monitor-to-find-a-user-mode-memory-leak"></a>使用性能监视器查找用户模式内存泄漏


如果您怀疑出现用户模式内存泄漏但不能确定哪个进程导致它，可以使用性能监视器来测量单个进程的内存使用情况。

启动性能监视器。 添加以下计数器：

-   **进程**--&gt;**专用字节数**（适用于你想要检查每个进程）

-   **进程**--&gt;**虚拟字节**（适用于你想要检查每个进程）

更改为 600 秒随着时间的推移捕获泄露的关系图的更新时间。 您可能想要将数据记录到一个文件以供日后检查。

**专用字节数**计数器指示进程已分配，不包括与其他进程共享的内存的内存总量。 **虚拟字节**计数器指示进程正在使用的虚拟地址空间的当前大小。

某些内存泄漏显示在增加数据文件中分配的专用字节数。 增加虚拟地址空间中的其他内存泄漏显示设置。

确定哪个进程正在泄漏内存之后，使用 UMDH 工具来确定有故障的特定例程。 有关详细信息，请参阅[查找用户模式内存泄漏到使用 UMDH](using-umdh-to-find-a-user-mode-memory-leak.md)。

 

 






---
title: 调试内核连接循环波特率
description: 调试内核连接循环波特率
keywords:
- 调试内核连接循环波特率
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f64b9d33eb3a2751ba4629e27a87d176ed161d25
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823411"
---
# <a name="debug--kernel-connection--cycle-baud-rate"></a>调试 | 内核连接 | 循环波特率


## <span id="ddk_debug_kernel_connection_cycle_baud_rate_dbg"></span><span id="DDK_DEBUG_KERNEL_CONNECTION_CYCLE_BAUD_RATE_DBG"></span>


指向 "**内核连接**"，然后单击 "**调试**" 菜单上的 "**循环波特率**"，以更改内核调试连接中使用的波特率。

此命令等效于按 CTRL + ALT + A。  (还可以在 KD 中按 CTRL + A ) 

此命令将遍历内核调试连接的所有可用波特率。 支持的波特速率为19200、38400、57600和115200。 每次使用此命令时，将选择下一个波特率。 如果波特率已经在115200，则将其缩减为19200。

不能使用此命令来更改调试时的波特率。 主计算机和目标计算机的波特率必须匹配，并且你无法在不重新启动计算机的情况下更改目标计算机的波特率。 因此，只有在两台计算机尝试以不同速率进行通信时，才必须更改波特率。 在这种情况下，必须更改主机计算机的波特率，使其与目标计算机的波特率匹配。

 

 






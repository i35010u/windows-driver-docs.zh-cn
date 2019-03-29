---
title: 调试内核连接周期的波特率
description: 调试内核连接周期的波特率
ms.assetid: 5d7f13ff-738d-498c-88cb-ad2d6fe596ac
keywords:
- 调试内核连接周期的波特率
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f611063e3a6207db1cddb9017b08b2a3bf9a21d5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563174"
---
# <a name="debug--kernel-connection--cycle-baud-rate"></a>调试 | 内核连接 | 循环波特率


## <span id="ddk_debug_kernel_connection_cycle_baud_rate_dbg"></span><span id="DDK_DEBUG_KERNEL_CONNECTION_CYCLE_BAUD_RATE_DBG"></span>


指向**内核连接**，然后单击**周期波特率**上**调试**菜单来更改在内核调试连接中使用的波特率。

此命令相当于按 CTRL + ALT + A。 （您可以还按 CTRL + A 中 KD。）

此命令进行循环的内核调试连接的所有可用波特率。 受支持的波特率有 19200、 38400、 57600 和 115200。 使用此命令中，每次选择下一步的波特率。 如果已经是 115200 波特率，则将其减少到 19200。

此命令不能用于更改在其中进行调试的波特率。 在主计算机和目标计算机的波特率必须匹配，并且不能无需重新启动计算机更改的目标计算机的波特率。 因此，两台计算机尝试以不同速率进行通信时，才必须更改的波特率。 在这种情况下，必须更改主计算机的波特率以匹配的目标计算机。

 

 






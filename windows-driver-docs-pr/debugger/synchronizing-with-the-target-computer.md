---
title: 与目标计算机同步
description: 与目标计算机同步
ms.assetid: bc9bbe35-6665-49ee-ba95-16ff03e25e96
keywords:
- 与目标计算机同步
- 与目标计算机中，同步概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e739d249ee1356490e7166413055894b1e2427f9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368139"
---
# <a name="synchronizing-with-the-target-computer"></a>与目标计算机同步


## <span id="ddk_synchronizing_with_the_target_computer_dbg"></span><span id="DDK_SYNCHRONIZING_WITH_THE_TARGET_COMPUTER_DBG"></span>


有时在内核模式调试，目标计算机停止响应到调试器。

在 KD，可以按[ **CTRL + R （重新同步）** ](ctrl-r--re-synchronize-.md) ，然后按 ENTER 与目标计算机进行同步。 在 WinDbg 中，使用[CTRL + ALT + R](debug---kernel-connection---resynchronize.md)或调试 |内核连接 |重新同步。

这些命令经常还原主机和目标之间的通信。 但是，重新同步可能始终会失败，尤其是当使用的 1394年内核连接。

[ **.Restart （重新启动内核连接）** ](-restart--restart-kernel-connection-.md)命令提供了更有效的方法的重新同步。 此命令相当于退出调试器，然后将新的调试器附加到现有会话。 此命令将仅在 KD 中进行，而不在 WinDbg 中。

**.Restart**执行时，命令是最有用[remote.exe 通过远程调试](remote-debugging-through-remote-exe.md)。 （在此类型的调试，可能会很难终止并重新启动调试器。）但是，不能使用 **.restart**从调试客户端，如果您正在执行通过调试器的远程调试。

 

 






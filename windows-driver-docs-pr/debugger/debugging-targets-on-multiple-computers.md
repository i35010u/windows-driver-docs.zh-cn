---
title: 在多台计算机上调试目标
description: 在多台计算机上调试目标
ms.assetid: 3c4fa2d9-1443-4460-b570-9415a3600393
keywords:
- 多个计算机调试
- 系统中，多台计算机上的目标
- 远程调试，多台计算机
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90b6fb0725150b2cf8e317169a2fea2beb9508b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350570"
---
# <a name="debugging-targets-on-multiple-computers"></a>在多台计算机上调试目标


## <span id="ddk_debugging_targets_on_multiple_computers_dbg"></span><span id="DDK_DEBUGGING_TARGETS_ON_MULTIPLE_COMPUTERS_DBG"></span>


调试器可以调试多个转储文件，或在同一时间实时用户模式应用程序。 请参阅[调试多个目标](debugging-multiple-targets.md)有关详细信息。

即使进程都位于不同的系统上，您可以调试多个实时目标。 只需在每个系统上，启动进程服务器，然后使用 **-premote**参数与[ **.attach （附加到进程）** ](-attach--attach-to-process-.md)或者[ **。创建 （创建进程）** ](-create--create-process-.md)来标识正确的进程服务器。

*当前*或*active*系统是当前正在调试的系统。 如果您使用 **.attach**或 **.create**再次而无需指定命令 **-premote**参数，调试器将附加到，或创建当前系统上的进程。

有关如何控制此类在调试会话的详细信息，请参阅[调试多个目标](debugging-multiple-targets.md)。

 

 






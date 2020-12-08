---
title: 在多台计算机上调试目标
description: 在多台计算机上调试目标
keywords:
- 多计算机调试
- 系统，多台计算机上的目标
- 远程调试，多台计算机
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c8b9a558119da81a267a4d9e3b56409ce3a2d2b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839165"
---
# <a name="debugging-targets-on-multiple-computers"></a>在多台计算机上调试目标


## <span id="ddk_debugging_targets_on_multiple_computers_dbg"></span><span id="DDK_DEBUGGING_TARGETS_ON_MULTIPLE_COMPUTERS_DBG"></span>


调试器可以同时调试多个转储文件或实时用户模式应用程序。 有关详细信息，请参阅 [调试多个目标](debugging-multiple-targets.md) 。

即使进程在不同的系统上，也可以调试多个实时目标。 只需在每个系统上启动进程服务器，然后将 **-premote** 参数与 [**. attach (附加到进程)**](-attach--attach-to-process-.md) 或 [**。创建 (创建进程)**](-create--create-process-.md) 来识别正确的进程服务器。

*当前* 或 *活动* 系统是当前正在调试的系统。 如果在未指定 **-premote** 参数的情况下再次使用 **attach** 或 **. create** 命令，调试器将附加到当前系统上的进程或创建进程。

有关如何控制此类调试会话的详细信息，请参阅 [调试多个目标](debugging-multiple-targets.md)。

 

 






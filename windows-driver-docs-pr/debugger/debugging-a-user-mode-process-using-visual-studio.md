---
title: 调试使用 Visual Studio 的用户模式进程
description: 在 Microsoft Visual Studio 中，可以使用 Windows 用户模式调试器附加到正在运行的进程或重新生成并附加到新的进程。
ms.assetid: C19D1B6F-B97B-4C1B-AD84-AC974C5F5C8C
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8f04f48700e6a6633d84e8be61ec6bb2faedf155
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547512"
---
# <a name="span-iddebuggerdebuggingauser-modeprocessusingvisualstudiospandebugging-a-user-mode-process-using-visual-studio"></a><span id="debugger.debugging_a_user-mode_process_using_visual_studio"></span>调试使用 Visual Studio 的用户模式进程

> [!IMPORTANT]
> 此功能不在 Windows 10，版本 1507年和更高版本的 WDK 中可用。
>

在 Microsoft Visual Studio 中，可以使用 Windows 用户模式调试器附加到正在运行的进程或重新生成并附加到新的进程。 进程可以运行调试器，运行在同一计算机上或者它可以在单独的计算机上运行。

本主题中所示的步骤要求具有集成到 Visual Studio Windows 驱动程序工具包。 要获取的集成的环境，请首先安装 Visual Studio 中，然后再安装 Windows Driver Kit (WDK)。 有关详细信息，请参阅[Windows Driver Kit (WDK)](https://go.microsoft.com/fwlink/p?linkid=391063)。

## <a name="span-idattachingtoarunningprocessonthesamecomputerspanspan-idattachingtoarunningprocessonthesamecomputerspanspan-idattachingtoarunningprocessonthesamecomputerspanattaching-to-a-running-process-on-the-same-computer"></a><span id="Attaching_to_a_running_process_on_the_same_computer"></span><span id="attaching_to_a_running_process_on_the_same_computer"></span><span id="ATTACHING_TO_A_RUNNING_PROCESS_ON_THE_SAME_COMPUTER"></span>将附加到同一台计算机上正在运行的进程


1.  在 Visual Studio 中，从**工具**菜单中，选择**附加到进程**。
2.  在中**附加到进程**对话框中，将**传输**到**Windows 用户模式调试器**，并设置**限定符**到**Localhost**。
3.  在中**可用进程**列表中，选择你想要将附加到的进程。
4.  单击**附加**。

### <a name="span-idnoninvasivedebuggingspanspan-idnoninvasivedebuggingspanspan-idnoninvasivedebuggingspannoninvasive-debugging"></a><span id="Noninvasive_debugging"></span><span id="noninvasive_debugging"></span><span id="NONINVASIVE_DEBUGGING"></span>非侵入调试

如果你想要调试正在运行的进程，仅在最低程度会影响在其执行中，应调试进程[noninvasively](noninvasive-debugging--user-mode-.md)。

## <a name="span-idspawninganewprocessonthesamecomputerspanspan-idspawninganewprocessonthesamecomputerspanspan-idspawninganewprocessonthesamecomputerspanspawning-a-new-process-on-the-same-computer"></a><span id="Spawning_a_new_process_on_the_same_computer"></span><span id="spawning_a_new_process_on_the_same_computer"></span><span id="SPAWNING_A_NEW_PROCESS_ON_THE_SAME_COMPUTER"></span>生成新的进程在同一计算机上


1.  在 Visual Studio 中，从**工具**菜单中，选择**调试器下启动**。
2.  在中**调试器下启动**对话框框中，输入可执行文件的路径。 您还可以输入自变量和工作目录。
3.  单击**启动。**

调试器创建 （也称为生成的进程） 的进程的行为稍有不同于调试器不会创建的进程。

而不是使用标准堆 API，调试器创建的进程使用特殊的调试堆。 你可以强制执行生成的进程，而不是调试堆中通过使用标准堆\_否\_调试\_堆环境变量。

此外，由于目标应用程序是在调试器的子进程，它将继承的调试程序的权限。 此权限可能会使目标应用程序来执行其否则无法执行某些操作。 例如，目标应用程序可能能够影响受保护的进程。

## <a name="span-idattachingtoarunningprocessonaseparatecomputerspanspan-idattachingtoarunningprocessonaseparatecomputerspanspan-idattachingtoarunningprocessonaseparatecomputerspanattaching-to-a-running-process-on-a-separate-computer"></a><span id="Attaching_to_a_running_process_on_a_separate_computer"></span><span id="attaching_to_a_running_process_on_a_separate_computer"></span><span id="ATTACHING_TO_A_RUNNING_PROCESS_ON_A_SEPARATE_COMPUTER"></span>将附加到不同的计算机上正在运行的进程


有时调试器和正在调试的代码运行单独的计算机上。 运行调试器的计算机称为*主机计算机*，并运行正在调试的代码的计算机称为*目标计算机*。 在主计算机上，可以配置从 Visual Studio 的目标计算机。 配置目标计算机也称为*预配*目标计算机。 有关详细信息，请参阅[预配计算机以便进行驱动程序部署和测试 (WDK 8.1)](https://msdn.microsoft.com/library/windows/hardware/dn745909)。

设置目标计算机后，可以在主计算机上使用 Visual Studio，若要附加到目标计算机上运行的进程。

1.  主机计算机上，在 Visual Studio 中，从**工具**菜单中，选择**附加到进程**。
2.  在中**附加到进程**对话框中，将**传输**到**Windows 用户模式调试器**，并设置**限定符**到的目标的名称计算机。
3.  在中**可用进程**列表中，选择你想要将附加到的进程。
4.  单击**附加**。

**请注意**  如果使用单独的主机和目标计算机时，不要安装 Visual Studio 和 WDK 目标计算机上。 如果在目标计算机上安装 Visual Studio 和 WDK 不支持调试。

 

 

 






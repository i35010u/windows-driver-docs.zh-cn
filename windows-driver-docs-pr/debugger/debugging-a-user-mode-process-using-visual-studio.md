---
title: 使用 Visual Studio 调试用户模式进程
description: 在 Microsoft Visual Studio 中，可以使用 Windows 用户模式调试器附加到正在运行的进程，或者生成并附加到新进程。
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7429826e5ed0cd3375a4948d4fa7e626b72687d4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819197"
---
# <a name="span-iddebuggerdebugging_a_user-mode_process_using_visual_studiospandebugging-a-user-mode-process-using-visual-studio"></a><span id="debugger.debugging_a_user-mode_process_using_visual_studio"></span>使用 Visual Studio 调试用户模式进程

> [!IMPORTANT]
> 此功能在 Windows 10 版本1507及更高版本的 WDK 中不可用。
>

在 Microsoft Visual Studio 中，可以使用 Windows 用户模式调试器附加到正在运行的进程，或者生成并附加到新进程。 该进程可以在运行调试器的同一台计算机上运行，也可以在单独的计算机上运行。

本主题中所示的过程要求将 Windows 驱动程序工具包集成到 Visual Studio 中。 若要获取集成环境，请首先安装 Visual Studio，然后 (WDK) 安装 Windows 驱动程序工具包。 有关详细信息，请参阅 [Windows 驱动程序工具包 (WDK) ](../index.yml)。

## <a name="span-idattaching_to_a_running_process_on_the_same_computerspanspan-idattaching_to_a_running_process_on_the_same_computerspanspan-idattaching_to_a_running_process_on_the_same_computerspanattaching-to-a-running-process-on-the-same-computer"></a><span id="Attaching_to_a_running_process_on_the_same_computer"></span><span id="attaching_to_a_running_process_on_the_same_computer"></span><span id="ATTACHING_TO_A_RUNNING_PROCESS_ON_THE_SAME_COMPUTER"></span>附加到同一计算机上正在运行的进程


1.  在 Visual Studio 的 " **工具** " 菜单中，选择 " **附加到进程**"。
2.  在 " **附加到进程** " 对话框中，设置 " **传输** 到 **Windows 用户模式调试器**"，并将 " **限定符** " 设置为 **Localhost**。
3.  在 " **可用进程** " 列表中，选择要附加到的进程。
4.  单击 **“附加”** 。

### <a name="span-idnoninvasive_debuggingspanspan-idnoninvasive_debuggingspanspan-idnoninvasive_debuggingspannoninvasive-debugging"></a><span id="Noninvasive_debugging"></span><span id="noninvasive_debugging"></span><span id="NONINVASIVE_DEBUGGING"></span>Noninvasive 调试

如果希望调试正在运行的进程，并且仅影响其执行的最小操作，则应调试进程 [noninvasively](noninvasive-debugging--user-mode-.md)。

## <a name="span-idspawning_a_new_process_on_the_same_computerspanspan-idspawning_a_new_process_on_the_same_computerspanspan-idspawning_a_new_process_on_the_same_computerspanspawning-a-new-process-on-the-same-computer"></a><span id="Spawning_a_new_process_on_the_same_computer"></span><span id="spawning_a_new_process_on_the_same_computer"></span><span id="SPAWNING_A_NEW_PROCESS_ON_THE_SAME_COMPUTER"></span>在同一台计算机上生成新进程


1.  在 Visual Studio 的 " **工具** " 菜单中，选择 " **在调试器下启动"**。
2.  在 " **在调试器下启动** " 对话框中，输入可执行文件的路径。 还可以输入参数和工作目录。
3.  单击 " **启动"。**

调试器创建的进程 (也称为生成进程) 与调试器不创建的进程的行为稍有不同。

调试器创建的进程使用特殊的调试堆，而不是使用标准堆 API。 您可以通过使用 " \_ 无 \_ 调试堆" 环境变量强制生成的进程使用标准堆而不是调试堆 \_ 。

此外，由于目标应用程序是调试器的子进程，因此它将继承调试器的权限。 此权限可能会使目标应用程序执行某些无法执行的操作。 例如，目标应用程序可能会影响受保护的进程。

## <a name="span-idattaching_to_a_running_process_on_a_separate_computerspanspan-idattaching_to_a_running_process_on_a_separate_computerspanspan-idattaching_to_a_running_process_on_a_separate_computerspanattaching-to-a-running-process-on-a-separate-computer"></a><span id="Attaching_to_a_running_process_on_a_separate_computer"></span><span id="attaching_to_a_running_process_on_a_separate_computer"></span><span id="ATTACHING_TO_A_RUNNING_PROCESS_ON_A_SEPARATE_COMPUTER"></span>在单独的计算机上附加到正在运行的进程


有时调试器和正在调试的代码在单独的计算机上运行。 运行调试器的计算机称为 *主机计算机*，运行正在调试的代码的计算机称为 *目标计算机*。 你可以在主计算机上从 Visual Studio 配置目标计算机。 配置目标计算机也称为 *预配* 目标计算机。 有关详细信息，请参阅[预配计算机以便进行驱动程序部署和测试 (WDK 8.1)](../gettingstarted/provision-a-target-computer-wdk-8-1.md)。

设置目标计算机后，你可以使用主计算机上的 Visual Studio 附加到在目标计算机上运行的进程。

1.  在主计算机上，在 Visual Studio 的 " **工具** " 菜单中，选择 " **附加到进程**"。
2.  在 " **附加到进程** " 对话框中，设置 " **传输** 到 **Windows 用户模式调试器**"，并将 " **限定符** " 设置为目标计算机的名称。
3.  在 " **可用进程** " 列表中，选择要附加到的进程。
4.  单击 **“附加”** 。

**注意**  
如果你使用的是单独的主机和目标计算机，请不要在目标计算机上安装 Visual Studio 和 WDK。 如果在目标计算机上安装了 Visual Studio 和 WDK，则不支持调试。

 

 


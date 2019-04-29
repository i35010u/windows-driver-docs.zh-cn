---
title: 在 Visual Studio 中设置用户模式调试
description: Microsoft Visual Studio 环境中有两个用户模式调试程序。
ms.assetid: D36220DF-1ACB-4D8B-BC4C-1A6FCB54CA15
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5ca46bafc45a4a507148ccbf049c2d5caef408e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368116"
---
# <a name="span-iddebuggersettingupuser-modedebugginginvisualstudiospansetting-up-user-mode-debugging-in-visual-studio"></a><span id="debugger.setting_up_user-mode_debugging_in_visual_studio"></span>设置 Visual Studio 中的用户模式下调试


Microsoft Visual Studio 环境中有两个用户模式调试程序。 一个是包含在为 Windows 调试工具，Windows 用户模式下调试程序。 另一个是 Visual Studio 调试器，它是 Visual Studio 产品的一部分。 本主题介绍如何完成设置以使用 Windows 用户模式下的调试器从 Visual Studio 环境中。

> [!IMPORTANT]
> 此功能不在 Windows 10，版本 1507年和更高版本的 WDK 中可用。
>

## <a name="span-iddebuggingauser-modeprocessonthelocalcomputerspanspan-iddebuggingauser-modeprocessonthelocalcomputerspanspan-iddebuggingauser-modeprocessonthelocalcomputerspandebugging-a-user-mode-process-on-the-local-computer"></a><span id="Debugging_a_User-Mode_Process_on_the_Local_Computer"></span><span id="debugging_a_user-mode_process_on_the_local_computer"></span><span id="DEBUGGING_A_USER-MODE_PROCESS_ON_THE_LOCAL_COMPUTER"></span>调试本地计算机上的用户模式进程


调试本地计算机上的用户模式进程所必需的任何特殊设置不。 有关附加到进程或启动的进程在调试器下的信息，请参阅[调试用户模式进程使用 Visual Studio](debugging-a-user-mode-process-using-visual-studio.md)。

## <a name="span-iddebuggingauser-modeprocessonatargetcomputerspanspan-iddebuggingauser-modeprocessonatargetcomputerspanspan-iddebuggingauser-modeprocessonatargetcomputerspandebugging-a-user-mode-process-on-a-target-computer"></a><span id="Debugging_a_User-Mode_Process_on_a_Target_Computer"></span><span id="debugging_a_user-mode_process_on_a_target_computer"></span><span id="DEBUGGING_A_USER-MODE_PROCESS_ON_A_TARGET_COMPUTER"></span>调试目标计算机上的用户模式进程


在某些情况下，两台计算机用于调试。 在运行调试程序*主机计算机*，并在代码上调试运行*目标计算机*。 在 Visual Studio 中 （在主计算机上运行），可以使用 Windows 用户模式下调试程序附加到目标计算机上的用户模式进程。

在目标计算机上转到**Control Panel&gt;网络和 Internet&gt;网络和共享中心&gt;高级共享设置**。 下**来宾或公共**，选择**启用网络发现**并**启用文件和打印机共享**。

您可以执行从主计算机的配置的其余部分：

1.  上，在 Visual Studio 中，主机计算机上**工具**菜单中，选择**附加到进程**。
2.  有关**传输**，选择**Windows 用户模式调试器**。
3.  右侧**限定符**框中，单击**浏览**按钮。
4.  单击“添加”按钮。
5.  输入目标计算机的名称。
6.  右侧**配置目标计算机**，单击**配置**按钮。 **配置目标计算机**对话框将打开并显示配置进度。
7.  当配置已完成，在**配置计算机**对话框中，单击**确定**。

 

 






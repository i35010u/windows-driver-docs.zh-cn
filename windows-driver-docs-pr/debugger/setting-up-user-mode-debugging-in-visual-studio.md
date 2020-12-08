---
title: 在 Visual Studio 中设置用户模式调试
description: Microsoft Visual Studio 环境中有两个用户模式调试器可用。
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 217739731424fe49025a03ede4e7b23640bbcc0d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836865"
---
# <a name="span-iddebuggersetting_up_user-mode_debugging_in_visual_studiospansetting-up-user-mode-debugging-in-visual-studio"></a><span id="debugger.setting_up_user-mode_debugging_in_visual_studio"></span>在 Visual Studio 中设置用户模式调试


Microsoft Visual Studio 环境中有两个用户模式调试器可用。 其中一种是 Windows User-Mode 调试器，它包含在 Windows 调试工具中。 另一个是 Visual Studio 调试器，它是 Visual Studio 产品的一部分。 本主题介绍如何在 Visual Studio 环境中设置使用 Windows User-Mode 调试程序。

> [!IMPORTANT]
> 此功能在 Windows 10 版本1507及更高版本的 WDK 中不可用。
>

## <a name="span-iddebugging_a_user-mode_process_on_the_local_computerspanspan-iddebugging_a_user-mode_process_on_the_local_computerspanspan-iddebugging_a_user-mode_process_on_the_local_computerspandebugging-a-user-mode-process-on-the-local-computer"></a><span id="Debugging_a_User-Mode_Process_on_the_Local_Computer"></span><span id="debugging_a_user-mode_process_on_the_local_computer"></span><span id="DEBUGGING_A_USER-MODE_PROCESS_ON_THE_LOCAL_COMPUTER"></span>调试本地计算机上的 User-Mode 进程


调试本地计算机上的用户模式进程不需要特殊设置。 有关附加到进程或在调试器下启动进程的信息，请参阅 [使用 Visual Studio 调试 User-Mode 进程](debugging-a-user-mode-process-using-visual-studio.md)。

## <a name="span-iddebugging_a_user-mode_process_on_a_target_computerspanspan-iddebugging_a_user-mode_process_on_a_target_computerspanspan-iddebugging_a_user-mode_process_on_a_target_computerspandebugging-a-user-mode-process-on-a-target-computer"></a><span id="Debugging_a_User-Mode_Process_on_a_Target_Computer"></span><span id="debugging_a_user-mode_process_on_a_target_computer"></span><span id="DEBUGGING_A_USER-MODE_PROCESS_ON_A_TARGET_COMPUTER"></span>在目标计算机上调试 User-Mode 进程


在某些情况下，两台计算机用于调试。 调试器在 *主计算机* 上运行，正在调试的代码在 *目标计算机* 上运行。 在 Visual Studio 中 () 上运行，你可以使用 Windows User-Mode 调试器附加到目标计算机上的用户模式进程。

在目标计算机上，中转到 **"控制面板" " &gt; 网络和 Internet &gt; 网络" 和 "共享中心 &gt; 高级共享设置**"。 在 " **来宾" 或 "公共**" 下，选择 " **启用网络发现** "，并 **打开 "文件和打印机共享**"。

你可以在主计算机上执行配置的其余部分：

1.  在主计算机上，在 Visual Studio 的 " **工具** " 菜单中，选择 " **附加到进程**"。
2.  对于 " **传输**"，请选择 " **Windows 用户模式调试器**"。
3.  在 " **限定符** " 框的右侧，单击 " **浏览** " 按钮。
4.  单击“添加”按钮。
5.  输入目标计算机的名称。
6.  在 " **配置目标计算机**" 的右侧，单击 " **配置** " 按钮。 此时将打开 " **配置目标计算机** " 对话框，并显示配置进度。
7.  配置完成后，在 " **配置计算机** " 对话框中，单击 **"确定"**。

 

 






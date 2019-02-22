---
title: GFlags 概述
description: GFlags 概述
ms.assetid: fa5c48bf-c0d0-4010-a101-381c692082bf
keywords:
- GFlags 概述
ms.date: 06/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 98d4e6f4ccc04420e4d9053445af6bd7d5cd2a54
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523821"
---
# <a name="gflags-overview"></a>GFlags 概述


## <span id="ddk_gflags_overview_dtools"></span><span id="DDK_GFLAGS_OVERVIEW_DTOOLS"></span>


GFlags (gflags.exe) 全局标志编辑器中，启用和禁用高级内部系统诊断和故障排除功能。 您可以从命令提示符窗口运行 GFlags 或使用其图形用户界面对话框。

有关如何安装和找到 gflags.exe 的信息，请参阅[GFlags](gflags.md)。


使用 GFlags 来激活以下功能：

<span id="Registry"></span><span id="registry"></span><span id="REGISTRY"></span>Registry  
设置系统级调试功能的计算机上运行的所有进程。 这些设置存储在**GlobalFlag**注册表项 (**HKEY\_本地\_机\\系统\\CurrentControlSet\\控件\\会话管理器\\GlobalFlag**)。 当您重新启动 Windows 并进行更改并再次重启之前保持有效，它们才会生效。

<span id="Kernel_flag_settings"></span><span id="kernel_flag_settings"></span><span id="KERNEL_FLAG_SETTINGS"></span>内核标志设置  
设置为此会话中调试功能。 这些设置将立即生效，但 Windows 关闭时都将丢失。 设置会影响此命令完成后启动的所有进程。

<span id="Image_file_settings"></span><span id="image_file_settings"></span><span id="IMAGE_FILE_SETTINGS"></span>图像文件设置  
设置调试特定程序的功能。 这些设置存储在每个程序 GlobalFlag 注册表项 (**HKEY\_本地\_机\\软件\\Microsoft\\ Windows NT\\ CurrentVersion\\图像 File Execution Options\\ *映像文件名*\\ GlobalFlag**)。 当您重新启动该程序并保持有效，直到更改它们，它们才会生效。

<span id="Debugger"></span><span id="debugger"></span><span id="DEBUGGER"></span>调试器  
指定特定程序始终在调试器中运行。 此设置存储在注册表中。 它将立即生效，并在更改之前保持有效。 (此功能目前仅在**全局标志**对话框。)

<span id="Launch"></span><span id="launch"></span><span id="LAUNCH"></span>启动  
使用指定的调试设置运行程序。 调试设置会有效，直到程序停止运行。 (此功能则仅可从**全局标志**对话框。)

<span id="Special_Pool"></span><span id="special_pool"></span><span id="SPECIAL_POOL"></span>特殊的池  
请求分配了指定的池标记或具有指定大小的将通过特殊池进行填充。 此功能可帮助你检测和识别内核池使用，例如超出了分配的内存空间中，编写或引用已释放的内存中的错误的源。

从 Windows Vista 开始，你可以启用、 禁用和配置特殊池功能 (**内核特殊池标记**) 作为内核标志设置，不需要重新启动，或注册表设置，这需要重新启动。

<span id="Page_heap_verification"></span><span id="page_heap_verification"></span><span id="PAGE_HEAP_VERIFICATION"></span>页堆验证  
启用、 禁用和配置页堆验证程序。 启用后，页面堆监视动态堆内存的操作，包括分配和可用的操作，并检测到堆错误时，会导致调试器中断。

<span id="Silent_process_exit"></span><span id="silent_process_exit"></span><span id="SILENT_PROCESS_EXIT"></span>无提示的进程退出  
启用、 禁用和配置监视和报告的无提示退出进程。 您可以指定在进程退出以无提示方式，包括通知、 事件日志记录和创建转储文件时，发生的操作。 有关详细信息，请参阅[监视无提示的进程退出](registry-entries-for-silent-process-exit.md)。

 

 






---
title: GFlags 概述
description: GFlags 概述
keywords:
- GFlags，概述
ms.date: 06/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: d9fa086790876ce685f10a60a03a207994c7c12e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834733"
---
# <a name="gflags-overview"></a>GFlags 概述


## <span id="ddk_gflags_overview_dtools"></span><span id="DDK_GFLAGS_OVERVIEW_DTOOLS"></span>


GFlags ( # A0) ，全局标志编辑器，启用和禁用高级内部系统诊断和故障排除功能。 你可以从命令提示符窗口运行 GFlags，或使用其图形用户界面对话框。

有关如何安装和查找 gflags.exe 的信息，请参阅 [GFlags](gflags.md)。


使用 GFlags 激活以下功能：

<span id="Registry"></span><span id="registry"></span><span id="REGISTRY"></span>Registry  
为计算机上运行的所有进程设置系统范围的调试功能。 这些设置存储在 **GlobalFlag** 注册表项中 (**HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ 控制 \\ 会话管理器 \\ GlobalFlag**) 。 它们会在重新启动 Windows 时生效并保持有效，直到你更改它们并再次重新启动。

<span id="Kernel_flag_settings"></span><span id="kernel_flag_settings"></span><span id="KERNEL_FLAG_SETTINGS"></span>内核标志设置  
为此会话设置调试功能。 这些设置将立即生效，但在 Windows 关闭时将丢失。 这些设置会影响在此命令完成后启动的所有进程。

<span id="Image_file_settings"></span><span id="image_file_settings"></span><span id="IMAGE_FILE_SETTINGS"></span>图像文件设置  
设置特定程序的调试功能。 这些设置存储在 GlobalFlag 注册表项中，每个程序 (**HKEY \_ 本地 \_ 计算机 \\ 软件 \\ Microsoft \\ Windows NT \\ CurrentVersion \\ 映像文件执行选项 \\ *ImageFileName* \\ GlobalFlag**) 。 它们会在你重新启动程序时生效并保持有效，直到你更改它们为止。

<span id="Debugger"></span><span id="debugger"></span><span id="DEBUGGER"></span>程序  
指定特定程序始终在调试器中运行。 此设置存储在注册表中。 它会立即生效并保持有效，直到你更改它。  (此功能仅在 " **全局标志** " 对话框中可用。 ) 

<span id="Launch"></span><span id="launch"></span><span id="LAUNCH"></span>开始  
使用指定的调试设置运行程序。 调试设置在程序停止之前有效。  (此功能仅在 " **全局标志** " 对话框中可用。 ) 

<span id="Special_Pool"></span><span id="special_pool"></span><span id="SPECIAL_POOL"></span>特殊池  
请求使用指定的池标记或指定大小的分配从特殊池填充。 此功能可帮助检测和确定内核池使用中的错误源，如写入超出分配的内存空间，或引用已释放的内存。

从 Windows Vista 开始，可以启用、禁用和配置特殊池功能 (**内核特殊池标记**) 作为内核标志设置，该设置不需要重新启动，也不需要重启。

<span id="Page_heap_verification"></span><span id="page_heap_verification"></span><span id="PAGE_HEAP_VERIFICATION"></span>页堆验证  
为程序启用、禁用和配置页堆验证。 启用后，页堆会监视动态堆内存操作（包括分配和自由操作），并在检测到堆错误时导致调试器中断。

<span id="Silent_process_exit"></span><span id="silent_process_exit"></span><span id="SILENT_PROCESS_EXIT"></span>无提示进程退出  
为进程启用、禁用和配置无提示退出的监视和报告。 可以指定在进程无提示退出时发生的操作，包括通知、事件日志记录和转储文件的创建。 有关详细信息，请参阅 [监视无提示进程退出](registry-entries-for-silent-process-exit.md)。

 

 






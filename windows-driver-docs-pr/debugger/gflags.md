---
title: GFlags
description: GFlags (全局标志编辑器) ，gflags.exe，启用和禁用高级调试、诊断和故障排除功能。
keywords: GFlags、全局标志编辑器 gflags.exe
ms.date: 06/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 116171842a14bf051863773cdad75db4544dcedb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834723"
---
# <a name="gflags"></a>GFlags


GFlags (全局标志编辑器) ，gflags.exe，启用和禁用高级调试、诊断和故障排除功能。 它通常用于打开其他工具跟踪、计数和日志的指示器。

## <a name="span-idwhere_to_get_gflagsspanspan-idwhere_to_get_gflagsspanspan-idwhere_to_get_gflagsspanwhere-to-get-gflags"></a><span id="Where_to_get_GFlags"></span><span id="where_to_get_gflags"></span><span id="WHERE_TO_GET_GFLAGS"></span>从何处获取 GFlags


GFlags 在 [适用于 Windows 10 (WinDbg) 的调试工具 ](debugger-download-tools.md)中包含。

安装调试工具之后，默认情况下，将在64位 Windows 上使用 gflags.exe 安装到以下目录中。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64
```

如果运行的是32位版本的 Windows，请使用此处 gflags.exe 32 位版本的。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86
```


## <a name="span-idddk_gflags_dtoolsspanspan-idddk_gflags_dtoolsspanoverview-of-gflags"></a><span id="ddk_gflags_dtools"></span><span id="DDK_GFLAGS_DTOOLS"></span>GFlags 概述


驱动程序开发人员和测试人员通常使用 GFlags 来打开调试、记录和测试功能，无论是直接的还是在测试脚本中包含 GFlags 命令。 页堆验证功能可帮助您确定内核模式驱动程序中的内存泄漏和缓冲区错误。

GFlags 有一个对话框和一个命令行界面。 大多数功能都可从两个接口获取，但某些功能只能从一个接口进行访问。  (参阅 [GFlags 详细信息](gflags-details.md)。 ) 

### <a name="span-idnew_featuresspanspan-idnew_featuresspanfeatures"></a><span id="new_features"></span><span id="NEW_FEATURES"></span>特征

-   页堆验证。 GFlags 现在包括 PageHeap 的函数 ( # A0) ，这是一种启用堆分配监视的工具。 PageHeap 包含在以前版本的 Windows 中。

-   特殊池功能无需重新启动。 在 Windows Vista 和更高版本的 Windows 上，你可以启用、禁用和配置特殊池功能，而无需重新启动 ) 计算机上 ( "重新启动"。 有关信息，请参阅 [特殊池](special-pool.md)。

-   对象引用跟踪。 新标志用于在内核中跟踪对象引用和对象取消引用。 Windows 的这一新功能检测到对象引用计数减少了太多次或未减少，即使不再使用某个对象。 只有 Windows Vista 和更高版本的 Windows 支持此标志。

-   新对话框设计。 GFlags 对话框具有选项卡式页面，便于导航。

### <a name="span-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="requirements"></span><span id="REQUIREMENTS"></span>要求

若要使用大多数 GFlags 功能，包括在注册表或内核模式下设置标志，或启用页堆验证，你必须是计算机上 Administrators 组的成员。 但是，在 Windows Vista 之前，具有至少来宾帐户访问权限的用户可以从 " **全局标志** " 对话框启动程序。

如果功能不起作用，或工作方式不同，则在特定操作系统版本上，该功能的说明中对这些差异进行了说明。

本主题包括以下内容：

[GFlags 概述](gflags-overview.md)

[GFlags 详细信息](gflags-details.md)

[**GFlags 命令**](gflags-commands.md)

[GFlags 标志表](gflags-flag-table.md)

[GFlags 和 PageHeap](gflags-and-pageheap.md)

[全局标志对话框](global-flags-dialog-box.md)

[GFlags 示例](gflags-examples.md)

[全局标志参考](global-flag-reference.md)

**注意**   不正确地使用此工具可能会降低系统性能或阻止 Windows 启动，要求你重新安装 Windows。

 

**重要提示**  在 windows Server 2003 和更高版本的 Windows （包括 Windows Vista）上永久启用了池标记。 在这些系统中，"**全局标志**" 对话框上的 "**启用池标记**" 复选框将灰显，启用或禁用池标记的命令将失败。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[Windows 调试工具中包含的工具](extra-tools.md)

 

 







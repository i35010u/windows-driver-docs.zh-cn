---
title: GFlags
description: GFlags （全局标志编辑器）、 gflags.exe、 启用和禁用高级调试、 诊断和故障排除功能。
ms.assetid: e268af2e-90a9-411e-8e29-ab486d2aac48
keywords: GFlags、 全局标志编辑器 gflags.exe
ms.date: 06/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: cfa08a777d1e4a9e5fd7c59687fb5a7f419aef18
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527202"
---
# <a name="gflags"></a>GFlags


GFlags （全局标志编辑器）、 gflags.exe、 启用和禁用高级调试、 诊断和故障排除功能。 它通常用于启用其他工具跟踪的指标、 计数和日志。

## <a name="span-idwheretogetgflagsspanspan-idwheretogetgflagsspanspan-idwheretogetgflagsspanwhere-to-get-gflags"></a><span id="Where_to_get_GFlags"></span><span id="where_to_get_gflags"></span><span id="WHERE_TO_GET_GFLAGS"></span>从中获取 GFlags


中包含 GFlags[调试 Windows 10 的工具 (WinDbg)](debugger-download-tools.md)。

安装调试工具后，在 64 位 Windows 上使用 gflags.exe 安装到以下目录的默认情况下。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64
```

如果正在运行 Windows 的 32 位版本，使用 gflags.exe 位于此处的 32 位版本。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86
```


## <a name="span-idddkgflagsdtoolsspanspan-idddkgflagsdtoolsspanoverview-of-gflags"></a><span id="ddk_gflags_dtools"></span><span id="DDK_GFLAGS_DTOOLS"></span>GFlags 的概述


驱动程序开发人员和测试人员通常使用 GFlags 启用调试，日志记录和测试功能，直接或通过测试脚本中包括 GFlags 命令。 页堆验证功能可帮助你确定内存泄漏和缓冲区内核模式驱动程序中的错误。

GFlags 具有一个对话框和命令行接口。 大多数功能可从这两个接口，但某些功能都可以访问从接口之一。 (请参阅[GFlags 详细信息](gflags-details.md)。)

### <a name="span-idnewfeaturesspanspan-idnewfeaturesspanfeatures"></a><span id="new_features"></span><span id="NEW_FEATURES"></span>功能

-   页堆验证。 GFlags 现在包括 PageHeap (pageheap.exe) 启用堆分配监视工具的函数。 PageHeap 曾在以前版本的 Windows。

-   所需的特殊池功能无需重新启动。 在 Windows Vista 和更高版本的 Windows 上，可以启用、 禁用和配置特殊池功能无需重新启动 （"重新启动"） 计算机。 有关信息，请参阅[特殊池](special-pool.md)。

-   对象引用跟踪。 新标志，则启用跟踪的对象引用和对象在内核中取消引用。 对象引用计数将递减次数过多或不减少，即使对象不再使用时，检测到这一新的 Windows 功能。 仅在 Windows Vista 和更高版本的 Windows 中支持此标志。

-   新的对话框框设计。 GFlags 对话框具有选项卡式页以便更易于导航。

### <a name="span-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="requirements"></span><span id="REQUIREMENTS"></span>要求

若要使用大多数 GFlags 功能，包括设置标志或内核模式或启用页堆验证注册表中必须是计算机上 Administrators 组的成员。 但是，在 Windows Vista 中，在具有用户之前至少来宾帐户访问权限可以启动将程序从此**全局标志**对话框。

当功能进行不起作用，或在特定操作系统版本上以不同的方式，工作时的功能说明中解释了这些差异。

本主题包括以下内容：

[GFlags 概述](gflags-overview.md)

[GFlags 详细信息](gflags-details.md)

[**GFlags 命令**](gflags-commands.md)

[GFlags 标志表](gflags-flag-table.md)

[GFlags 和 PageHeap](gflags-and-pageheap.md)

[全局标志对话框](global-flags-dialog-box.md)

[GFlags 示例](gflags-examples.md)

[全局标志引用](global-flag-reference.md)

**请注意**  不正确使用此工具可以降低系统性能或阻止 Windows 启动，而必须重新安装 Windows。

 

**重要**  标记池永久上启用了 Windows Server 2003 和更高版本的 Windows，其中包括 Windows Vista。 在这些系统上**启用池标记**上的复选框**全局标志**对话框为灰色，而命令来启用或禁用池标记失败。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[Windows 调试工具中包含的工具](extra-tools.md)

 

 







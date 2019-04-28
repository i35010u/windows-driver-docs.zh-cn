---
title: 读取移出页面的标头中的符号
description: 读取移出页面的标头中的符号
ms.assetid: 74ec20d8-e2b5-449d-8b93-7553c57fac07
keywords:
- 符号，调出标头的问题
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 267b6ef8d4ad4a9286e8601146cd056277cd12c3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350547"
---
# <a name="reading-symbols-from-paged-out-headers"></a>读取移出页面的标头中的符号


## <span id="ddk_reading_symbols_from_paged_out_headers_dbg"></span><span id="DDK_READING_SYMBOLS_FROM_PAGED_OUT_HEADERS_DBG"></span>


内核调试程序必须读取每个已加载的模块的映像的标的头，这样才能知道哪些符号对应于该模块。

如果模块的标头分页输出到磁盘，调试器将不会加载此模块的符号。 如果使用模块所需的关键到调试过程发生这种情况，它可以是严重问题。

可以使用以下过程来解决此问题。

**若要获取用于调出标头的符号**

1.  第二个复制一份内核本身。 它是可能最简单的方法将此代码放在网络共享上。

2.  将此共享的根目录到符号路径。 请参阅[符号路径](symbol-path.md)更改符号路径的方法。

3.  使用[ **.reload （重新加载模块）** ](-reload--reload-module-.md)命令。

4.  使用[ **！ 符号干扰**](-sym.md)扩展命令以查看更详细的输出。 如果使用，你将能够查看哪些符号加载从目标计算机上的模块映像和从内核模块的副本中加载的。

此方法必须使用时要小心，因为调试器具有无法验证是否实际文件副本与匹配的原始文件。 因此，重要的网络共享上使用的 Windows 版本与目标计算机上使用的版本相匹配。

此方法仅用于内核模式调试。 操作系统是分页的能够在用户模式下调试 （除非磁盘保存分页文件为已卸载，或者无法访问） 过程中所需的任何标头中。

下面是使用此技术的示例：

```dbgcmd
kd> .reload
Connected to Windows XP 2268 x86 compatible target, ptr64 FALSE
Loading Kernel Symbols
..........Unable to read image header for dmload.sys at fe0be000 - NTSTATUS 0xC0000001
..........Unable to read image header for dmboot.sys at fda93000 - NTSTATUS 0xC0000001
.....................................Unable to read image header for fdc.sys at fdfc2000 - NTSTATUS 0xC0000001
...Unable to read image header for flpydisk.sys at fde4a000 - NTSTATUS 0xC0000001
.Unable to read image header for Fs_Rec.SYS at fe0c8000 - NTSTATUS 0xC0000001
.Unable to read image header for Null.SYS at fe2c4000 - NTSTATUS 0xC0000001
...................Unable to read image header for win32k.sys at a0000000 - NTSTATUS 0xC0000001
..Unable to read image header for dxg.sys at a0194000 - NTSTATUS 0xC0000001
.......Unable to read image header for ati2draa.dll at a01a4000 - NTSTATUS 0xC0000001
..Unable to read image header for ParVdm.SYS at fe116000 - NTSTATUS 0xC0000001
.......
Loading unloaded module list
..............
Loading User Symbols
Unable to retrieve the PEB address. This is usually caused
by being in the wrong process context or by paging
```

请注意，许多映像不可访问的标头。 检查从这些文件之一的符号 (在此示例中，fs\_rec.sys):

```dbgcmd
kd> x fs_rec!*
*** ERROR: Module load completed but symbols could not be loaded for fs_rec.sys
```

这些标头显然调出。因此，您需要将适当的图像添加到符号路径：

```dbgcmd
kd> .sympath+ \\myserver\myshare\symbols\x86fre\symbols
Symbol search path is: symsrv*symsrv.dll*c:\localcache*https://msdl.microsoft.com/download/symbols;\\myserver\myshare\symbols\x86fre\symbols

kd> .reload
Connected to Windows XP 2268 x86 compatible target, ptr64 FALSE
Loading Kernel Symbols
..........Unable to read image header for dmload.sys at fe0be000 - NTSTATUS 0xC0000001
..........Unable to read image header for dmboot.sys at fda93000 - NTSTATUS 0xC0000001
.....................................Unable to read image header for fdc.sys at fdfc2000 - NTSTATUS 0xC0000001
...Unable to read image header for flpydisk.sys at fde4a000 - NTSTATUS 0xC0000001
.Unable to read image header for Fs_Rec.SYS at fe0c8000 - NTSTATUS 0xC0000001
.Unable to read image header for Null.SYS at fe2c4000 - NTSTATUS 0xC0000001
...................Unable to read image header for win32k.sys at a0000000 - NTSTATUS 0xC0000001
..Unable to read image header for dxg.sys at a0194000 - NTSTATUS 0xC0000001
.......Unable to read image header for ati2draa.dll at a01a4000 - NTSTATUS 0xC0000001
..Unable to read image header for ParVdm.SYS at fe116000 - NTSTATUS 0xC0000001
.......
Loading unloaded module list
..............
Loading User Symbols
Unable to retrieve the PEB address. This is usually caused
by being in the wrong process context or by paging
```

出现的警告，但符号本身现在均可访问：

```dbgcmd
kd> x fs_Rec!*
fe0c8358  Fs_Rec!_imp___allmul
fe0c8310  Fs_Rec!_imp__IoCreateDevice
fe0c835c  Fs_Rec!_imp___allshr
........
fe0c8360  Fs_Rec!ntoskrnl_NULL_THUNK_DATA
fe0c832c  Fs_Rec!_imp__KeSetEvent
fe0c9570  Fs_Rec!_NULL_IMPORT_DESCRIPTOR
```

 

 






---
title: 读取移出页面的标头中的符号
description: 读取移出页面的标头中的符号
keywords:
- 符号，分页的标头问题
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 238783f267ffdd5f5d611f44ba81336bcd4906fa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839155"
---
# <a name="reading-symbols-from-paged-out-headers"></a>读取移出页面的标头中的符号

内核调试器必须读取每个已加载模块的映像的标头，才能知道哪个符号对应于该模块。

如果模块的标头已分页到磁盘，调试器将不会加载此模块的符号。 如果对调试过程至关重要的模块发生这种情况，则可能是一个关键问题。

以下过程可用于解决此问题。

## <a name="to-acquire-symbols-for-paged-out-headers"></a>获取用于分页的标头的符号

1. 创建内核本身的第二个副本。 最简单的方法是将其放在网络共享上。

2. 将此共享的根目录追加到符号路径。 请参阅 [符号路径](symbol-path.md) 了解更改符号路径的方法。

3. 使用 [**. reload.sql (Reload.sql Module)**](-reload--reload-module-.md) 命令。

4. 使用 [**！符号干扰**](-sym.md) 扩展命令查看更详细的输出。 如果使用此模式，你将能够查看从目标计算机上的模块映像加载的符号，以及从内核模块的副本加载哪些符号。

必须谨慎使用此方法，因为调试器无法验证文件的复制是否与原始文件完全匹配。 因此，网络共享上使用的 Windows 版本与目标计算机上使用的版本匹配，这一点非常重要。

此方法仅用于内核模式调试。 操作系统能够在用户模式调试过程中所需的任何标头中分页 (除非已卸除包含页面文件的磁盘，否则) 无法访问该磁盘。

下面是使用此技术的一个示例：

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

请注意，许多映像具有不可访问的标头。 在此示例中，通过 fsrec.sys) 检查这些文件中的符号 (\_ ：

```dbgcmd
kd> x fs_rec!*
*** ERROR: Module load completed but symbols could not be loaded for fs_rec.sys
```

这些标头显然已分页。因此，需要将正确的映像添加到符号路径：

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

出现相同的警告，但现在可以访问符号本身：

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

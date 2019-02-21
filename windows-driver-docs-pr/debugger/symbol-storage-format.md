---
title: 符号存储格式
description: 符号存储格式
ms.assetid: 4aeaa644-9da4-4567-9dc7-86db38b7e93c
keywords:
- SymStore，存储格式
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8e0d2252edf1a1ee5aed505e448de3c04f25d33
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542525"
---
# <a name="symbol-storage-format"></a>符号存储格式


## <span id="ddk_symbol_files_overview_dbg"></span><span id="DDK_SYMBOL_FILES_OVERVIEW_DBG"></span>


SymStore 使用作为数据库文件系统本身。 它创建基于符号文件时间戳、 签名、 年龄和其他数据等内容的目录名称的目录，一个大型树。

例如，多个不同 acpi.dbgs 已添加到服务器后，目录可能如下所示：

```console
Directory of \\mybuilds\symsrv\acpi.dbg
10/06/1999  05:46p      <DIR>          .
10/06/1999  05:46p      <DIR>          ..
10/04/1999  01:54p      <DIR>          37cdb03962040
10/04/1999  01:49p      <DIR>          37cdb04027740
10/04/1999  12:56p      <DIR>          37e3eb1c62060
10/04/1999  12:51p      <DIR>          37e3ebcc27760
10/04/1999  12:45p      <DIR>          37ed151662060
10/04/1999  12:39p      <DIR>          37ed15dd27760
10/04/1999  11:33a      <DIR>          37f03ce962020
10/04/1999  11:21a      <DIR>          37f03cf7277c0
10/06/1999  05:38p      <DIR>          37fa7f00277e0
10/06/1999  05:46p      <DIR>          37fa7f01620a0
```

在此示例中，acpi.dbg 符号文件的查找路径可能如下所示： \\ \\mybuilds\\symsrv\\acpi.dbg\\37cdb03962040。

查找目录内可能存在三个文件：

1.  acpi.dbg，如果文件的存储

2.  file.ptr 替换为实际的符号文件，如果一个指针，存储路径

3.  refs.ptr，其中包含为具有此时间戳和图像大小 acpi.dbg 当前添加到符号存储区的所有最新位置的列表

显示的目录列表\\ \\mybuilds\\symsrv\\acpi.dbg\\37cdb03962040 提供了下列：

```console
10/04/1999  01:54p                  52 file.ptr
10/04/1999  01:54p                  67 refs.ptr
```

文件 file.ptr 包含文本字符串"\\\\mybuilds\\符号\\x86\\2128.chk\\符号\\sys\\acpi.dbg"。 由于没有此目录中名为 acpi.dbg 没有文件，调试器将尝试在找到文件\\ \\mybuilds\\符号\\x86\\2128.chk\\符号\\sys\\acpi.dbg。

Refs.ptr 的内容仅供 SymStore，而不是调试器。 此文件包含此目录中发生的所有事务的记录。 可能从 refs.ptr 一个示例行：

```text
0000000026,ptr,\\mybuilds\symbols\x86\2128.chk\symbols\sys\acpi.dbg
```

这段代码说明一个指向\\ \\mybuilds\\符号\\x86\\2128.chk\\符号\\sys\\acpi.dbg 添加了事务"0000000026"。

某些符号文件保持不变通过各种产品或生成或某一特定产品。 一个例子是 Windows 2000 文件 msvcrt.pdb。 目录列表\\ \\mybuilds\\symsrv\\msvcrt.pdb 显示只有两个版本的 msvcrt.pdb 已被添加到符号服务器：

```console
Directory of \\mybuilds\symsrv\msvcrt.pdb
10/06/1999  05:37p      <DIR>          .
10/06/1999  05:37p      <DIR>          ..
10/04/1999  11:19a      <DIR>          37a8f40e2
10/06/1999  05:37p      <DIR>          37f2c2272
```

但是的目录列表\\ \\mybuilds\\symsrv\\msvcrt.pdb\\37a8f40e2 显示该 refs.ptr 中有多个指针。

```console
Directory of \\mybuilds\symsrv\msvcrt.pdb\37a8f40e2
10/05/1999  02:50p              54     file.ptr
10/05/1999  02:50p           2,039     refs.ptr
```

内容\\ \\mybuilds\\symsrv\\msvcrt.pdb\\37a8f40e2\\refs.ptr 如下：

```text
0000000001,ptr,\\mybuilds\symbols\x86\2137\symbols\dll\msvcrt.pdb
0000000002,ptr,\\mybuilds\symbols\x86\2137.chk\symbols\dll\msvcrt.pdb
0000000003,ptr,\\mybuilds\symbols\x86\2138\symbols\dll\msvcrt.pdb
0000000004,ptr,\\mybuilds\symbols\x86\2138.chk\symbols\dll\msvcrt.pdb
0000000005,ptr,\\mybuilds\symbols\x86\2139\symbols\dll\msvcrt.pdb
0000000006,ptr,\\mybuilds\symbols\x86\2139.chk\symbols\dll\msvcrt.pdb
0000000007,ptr,\\mybuilds\symbols\x86\2140\symbols\dll\msvcrt.pdb
0000000008,ptr,\\mybuilds\symbols\x86\2140.chk\symbols\dll\msvcrt.pdb
0000000009,ptr,\\mybuilds\symbols\x86\2136\symbols\dll\msvcrt.pdb
0000000010,ptr,\\mybuilds\symbols\x86\2136.chk\symbols\dll\msvcrt.pdb
0000000011,ptr,\\mybuilds\symbols\x86\2135\symbols\dll\msvcrt.pdb
0000000012,ptr,\\mybuilds\symbols\x86\2135.chk\symbols\dll\msvcrt.pdb
0000000013,ptr,\\mybuilds\symbols\x86\2134\symbols\dll\msvcrt.pdb
0000000014,ptr,\\mybuilds\symbols\x86\2134.chk\symbols\dll\msvcrt.pdb
0000000015,ptr,\\mybuilds\symbols\x86\2133\symbols\dll\msvcrt.pdb
0000000016,ptr,\\mybuilds\symbols\x86\2133.chk\symbols\dll\msvcrt.pdb
0000000017,ptr,\\mybuilds\symbols\x86\2132\symbols\dll\msvcrt.pdb
0000000018,ptr,\\mybuilds\symbols\x86\2132.chk\symbols\dll\msvcrt.pdb
0000000019,ptr,\\mybuilds\symbols\x86\2131\symbols\dll\msvcrt.pdb
0000000020,ptr,\\mybuilds\symbols\x86\2131.chk\symbols\dll\msvcrt.pdb
0000000021,ptr,\\mybuilds\symbols\x86\2130\symbols\dll\msvcrt.pdb
0000000022,ptr,\\mybuilds\symbols\x86\2130.chk\symbols\dll\msvcrt.pdb
0000000023,ptr,\\mybuilds\symbols\x86\2129\symbols\dll\msvcrt.pdb
0000000024,ptr,\\mybuilds\symbols\x86\2129.chk\symbols\dll\msvcrt.pdb
0000000025,ptr,\\mybuilds\symbols\x86\2128\symbols\dll\msvcrt.pdb
0000000026,ptr,\\mybuilds\symbols\x86\2128.chk\symbols\dll\msvcrt.pdb
0000000027,ptr,\\mybuilds\symbols\x86\2141\symbols\dll\msvcrt.pdb
0000000028,ptr,\\mybuilds\symbols\x86\2141.chk\symbols\dll\msvcrt.pdb
0000000029,ptr,\\mybuilds\symbols\x86\2142\symbols\dll\msvcrt.pdb
0000000030,ptr,\\mybuilds\symbols\x86\2142.chk\symbols\dll\msvcrt.pdb
```

这将显示为 Windows 2000 上存储，适用的符号的多个版本使用同一 msvcrt.pdb \\ \\mybuilds\\symsrv。

下面是目录的包含文件和指针添加件的组合的示例：

```console
Directory of E:\symsrv\dbghelp.dbg\38039ff439000
10/12/1999  01:54p         141,232     dbghelp.dbg
10/13/1999  04:57p              49     file.ptr
10/13/1999  04:57p             306     refs.ptr
```

在这种情况下，refs.ptr 具有以下内容：

```text
0000000043,file,e:\binaries\symbols\retail\dll\dbghelp.dbg
0000000044,file,f:\binaries\symbols\retail\dll\dbghelp.dbg
0000000045,file,g:\binaries\symbols\retail\dll\dbghelp.dbg
0000000046,ptr,\\MyDir\bin\symbols\retail\dll\dbghelp.dbg
0000000047,ptr,\\foo2\bin\symbols\retail\dll\dbghelp.dbg
```

因此，事务 43、 44 和 45 相同文件添加到服务器和事务 46 和 47 添加指针。 如果删除事务 43、 44 和 45，则将从目录删除文件 dbghelp.dbg。 然后，目录将具有以下内容：

```console
Directory of e:\symsrv\dbghelp.dbg\38039ff439000
10/13/1999  05:01p                   49 file.ptr
10/13/1999  05:01p                 130 refs.ptr
```

现在 file.ptr 包含"\\\\foo2\\bin\\符号\\零售\\dll\\dbghelp.dbg"，并包含 refs.ptr

```text
0000000046,ptr,\\MyDir\bin\symbols\retail\dll\dbghelp.dbg
0000000047,ptr,\\foo2\bin\symbols\retail\dll\dbghelp.dbg
```

每当 refs.ptr 中的最后一项是指针，文件 file.ptr 将存在并包含关联的文件的路径。 每当 refs.ptr 中的最后一项是文件，将此目录中不存在任何 file.ptr。 因此，任何 refs.ptr 中移除的最后一项的删除操作可能会导致 file.ptr 正在创建、 删除或更改。

 

 






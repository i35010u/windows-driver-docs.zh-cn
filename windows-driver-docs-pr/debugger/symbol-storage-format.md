---
title: 符号存储格式
description: 符号存储格式
keywords:
- SymStore，存储格式
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22954b341587b13289c9015e3524f4650416eaef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813947"
---
# <a name="symbol-storage-format"></a>符号存储格式


## <span id="ddk_symbol_files_overview_dbg"></span><span id="DDK_SYMBOL_FILES_OVERVIEW_DBG"></span>


SymStore 使用文件系统本身作为数据库。 它创建了一个大型目录树，其中包含基于符号文件时间戳、签名、age 和其他数据这样的目录名称。

例如，在多个不同的 dbgs 已添加到服务器后，目录可能如下所示：

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

在此示例中，acpi 符号文件的查找路径可能如下所示： \\ \\ mybuilds \\ symsrv \\ acpi \\ 37cdb03962040。

查找目录中可能存在三个文件：

1.  如果文件已存储，则为 acpi

2.  文件 ptr，其中包含实际符号文件的路径（如果已存储指针）

3.  refs ptr，其中包含具有此时间戳的 acpi 的所有当前位置的列表以及当前已添加到符号存储区的映像大小

显示 \\ \\ mybuilds \\ symsrv acpi 37cdb03962040 的目录列表 \\ \\ 将提供以下内容：

```console
10/04/1999  01:54p                  52 file.ptr
10/04/1999  01:54p                  67 refs.ptr
```

文件. ptr 包含文本字符串 " \\ \\ mybuilds \\ 符号 \\ x86 \\ 2128 \\ \\ \\ ）"。 由于此目录中没有名为 acpi 的文件，因此调试器将尝试在 \\ \\ mybuilds \\ 符号 \\ x86 \\ 2128 \\ 符号 \\ sys \\ acpi。

Refs 的内容仅供 SymStore 使用，而不是由调试器使用。 此文件包含在此目录中发生的所有事务的记录。 来自 refs 的示例行。 ptr 可能是：

```text
0000000026,ptr,\\mybuilds\symbols\x86\2128.chk\symbols\sys\acpi.dbg
```

这表明，指向 \\ \\ mybuilds \\ 符号 \\ x86 2128 的指针 \\ \\ \\ \\ 已添加事务 "0000000026"。

某些符号文件在各种产品或内部版本或特定产品上保持不变。 Windows 2000 文件 msvcrt.lib 就是其中的一个示例。 \\ \\ Mybuilds symsrv msvcrt.lib 目录列表 \\ \\ 显示，只向符号服务器添加了两个版本的 msvcrt.lib：

```console
Directory of \\mybuilds\symsrv\msvcrt.pdb
10/06/1999  05:37p      <DIR>          .
10/06/1999  05:37p      <DIR>          ..
10/04/1999  11:19a      <DIR>          37a8f40e2
10/06/1999  05:37p      <DIR>          37f2c2272
```

但是， \\ \\ mybuilds \\ symsrv msvcrt.lib 37a8f40e2 的目录列表 \\ 显示了 \\ refs。 ptr 中有多个指针。

```console
Directory of \\mybuilds\symsrv\msvcrt.pdb\37a8f40e2
10/05/1999  02:50p              54     file.ptr
10/05/1999  02:50p           2,039     refs.ptr
```

\\ \\ Mybuilds \\ symsrv \\ msvcrt.lib \\ 37a8f40e2 refs 的内容如下所 \\ 示：

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

这表明，同一 msvcrt.lib 用于在 \\ \\ mybuilds \\ symsrv 上存储的 Windows 2000 符号的多个版本。

下面是包含混合文件和指针添加的目录的示例：

```console
Directory of E:\symsrv\dbghelp.dbg\38039ff439000
10/12/1999  01:54p         141,232     dbghelp.dbg
10/13/1999  04:57p              49     file.ptr
10/13/1999  04:57p             306     refs.ptr
```

在这种情况下，refs 具有以下内容：

```text
0000000043,file,e:\binaries\symbols\retail\dll\dbghelp.dbg
0000000044,file,f:\binaries\symbols\retail\dll\dbghelp.dbg
0000000045,file,g:\binaries\symbols\retail\dll\dbghelp.dbg
0000000046,ptr,\\MyDir\bin\symbols\retail\dll\dbghelp.dbg
0000000047,ptr,\\foo2\bin\symbols\retail\dll\dbghelp.dbg
```

因此，事务43、44和45向服务器中添加了相同的文件，并且事务46和47添加了指针。 如果删除事务43、44和45，则将从目录中删除 dbghelp.dll 文件。 然后，该目录将具有以下内容：

```console
Directory of e:\symsrv\dbghelp.dbg\38039ff439000
10/13/1999  05:01p                   49 file.ptr
10/13/1999  05:01p                 130 refs.ptr
```

现在，file. ptr 包含 " \\ \\ foo2 \\ bin \\ 符号 \\ retail \\ dll \\ dbghelp.dll"，而 refs 包含

```text
0000000046,ptr,\\MyDir\bin\symbols\retail\dll\dbghelp.dbg
0000000047,ptr,\\foo2\bin\symbols\retail\dll\dbghelp.dbg
```

只要 refs 中的最后一个条目是指针，文件就会存在，并包含指向关联文件的路径。 只要 refs 中的最后一个条目为文件，此目录中就不会存在任何文件。 因此，删除 refs 中最后一项的任何删除操作都可能会导致创建、删除或更改 ptr。

 

 






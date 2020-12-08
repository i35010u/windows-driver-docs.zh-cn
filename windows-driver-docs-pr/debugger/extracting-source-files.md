---
title: 提取源文件
description: 提取源文件
keywords:
- 提取源文件
- 源服务器，提取源文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66b28f17a74365eac4dabac1af1fa9ea7d6a0a79
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819187"
---
# <a name="extracting-source-files"></a>提取源文件


若要从所有需要为其提供源的模块中提取所有源文件，请使用命令：

```console
srctool.exe -x
```

此工具必须在具有版本控制访问权限的计算机上已为版本控制系统进行了源索引的 .pdb 文件中执行。 这会将所有源文件置于公用目录树中。 将此树的内容复制到网站的根目录。 您可以根据需要在任何要添加的新产品或模块上执行此操作。 由于目录树结构使不同的文件相互独立且可访问，因此没有任何担心文件会相互覆盖。

### <a name="span-idwalkspanspan-idwalkspanwalk"></a><span id="walk"></span><span id="WALK"></span>浏览

行走 (行走 .cmd) 脚本包含在适用于 Windows 的调试工具中。 此脚本会在目录树中以递归方式搜索，并对与指定的文件掩码匹配的任何文件执行任何指定的命令。 语法为：

```console
walk.cmd FileMask Command
```

其中， *FileMask* 指定一个带有或不带随附的起始目录的文件掩码，并且 *命令* 指定要执行的命令。

下面是一个示例，该示例对 c：符号中的所有 .pdb 文件及其子目录运行 srctool.exe 文件提取命令 \\ ：

```console
walk.cmd c:\symbols\*.pdb srctool.exe -x
```

 

 






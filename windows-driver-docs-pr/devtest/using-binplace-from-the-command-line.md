---
title: 从命令行使用 BinPlace
description: 从命令行使用 BinPlace
ms.assetid: ed92fee5-d45c-437a-8c3f-de51b910c2ae
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12c5fdb3b54fa7e01b969518a56bb614e679d242
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341635"
---
# <a name="using-binplace-from-the-command-line"></a>从命令行使用 BinPlace


**重要**  此主题中的示例讨论如何使用 BINPLACE\_PLACEFILE 宏和[BinPlace](binplace.md)[**位置文件**](place-file-syntax.md). 此宏和文件中的 Windows 驱动程序工具包的 Windows 7 版本已过时和 WDK 的未来版本中可能不支持。

 

本主题提供使用 BinPlace 从命令行中的示例。

首先，您可以按如下所示设置根目标目录：

```
set _NTTREE=d:\ProjectRoot
```

然后可以按以下方式设置位置文件的路径和文件名：

```
set BINPLACE_PLACEFILE=d:\mystuff\myplacefile.txt
```

允许的文件 d： 内容\\mystuff\\myplacefile.txt 是按如下所示：

```
; This is a simple place file.
commonmodule.dll   retail
application.exe    files\bin
mydriver.sys       *\drivertree
extra.cab          appendix
```

现在可以使用以下命令运行 BinPlace:

```
binplace g:\somelocation\extra.cab
```

由于 extra.cab 不是可执行文件，BinPlace 只能移动它。 根目标目录为 d:\\projectroot。 为在位置文件中指定此文件的类目录**附录**。 文件类型子目录是文件的 cab （正在移动的文件扩展名）。 因此，此文件复制到位置 d:\\projectroot\\附录\\cab\\extra.cab。

现在使用 BinPlace 可执行文件和其符号文件。 若要执行此操作，指定可执行文件的名称--BinPlace 将查找关联的符号文件。

当你将可执行文件名称传递给 BinPlace 时，它查找可执行文件所在的同一目录中其符号文件。 如果它找不到它们存在，它读取存储在可执行文件; 中的 CodeView 记录如果该记录中找到符号文件路径，它查找该路径中的符号文件。

**请注意**  显式指定符号文件名称，如果 BinPlace 将只是将其移动，不处理它。

 

```
binplace -a -x -s d:\stripped -n g:\full g:\builddir\application.exe
```

可执行文件使用的同一根目标目录为之前。 其类目录是文件\\bin。 因此，放置在 d:\\projectroot\\文件\\bin\\application.exe。

符号文件放置在两个位置。 完整符号文件 （包括专用和公共符号） 将转到 g:\\完整\\文件\\bin\\exe\\application.pdb。 去除的符号文件 （包含仅公共符号） 将转到 d:\\去除\\文件\\bin\\exe\\application.pdb。

现在，commonmodule.dll 上使用类似的命令：

```
binplace -a -x -s d:\stripped -n g:\full g:\builddir\commonmodule.dll
```

这一次，类子目录是**零售**。 对于可执行文件，此目录名称是"不使用类子目录中，"的代码以便它位于 d:\\projectroot\\application.exe。 符号文件将放入 g:\\完整\\零售\\dll\\application.pdb 和 d:\\去除\\零售\\dll\\application.pdb。

最后，使用上 mydriver.sys BinPlace 并省略 **-n**切换：

```
binplace -a -x -s d:\stripped g:\builddir\mydriver.sys
```

下面是类子目录 **\*/drivertree**。 可执行文件，星号 (\*) 将被替换为处理器类型。 假设您正在 x86 上运行的计算机，可执行文件放置在 d:\\projectroot\\i386\\drivertree\\application.exe。 去除的符号文件被放置在 g:\\完整\\drivertree\\sys\\application.pdb，因为星号忽略符号文件。 因为 **-n**开关被省略，完整的符号文件不位于任何位置。

 

 






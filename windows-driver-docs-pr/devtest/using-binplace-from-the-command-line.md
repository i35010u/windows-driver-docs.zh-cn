---
title: 从命令行使用 BinPlace
description: 从命令行使用 BinPlace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 296031f82de96c567058d641ee348b721cb0de5a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841273"
---
# <a name="using-binplace-from-the-command-line"></a>从命令行使用 BinPlace


**重要提示**  本主题中的示例介绍了 BINPLACE \_ PLACEFILE 宏和 [BINPLACE](binplace.md)[**位置文件**](place-file-syntax.md)的用法。 此宏和文件在 windows 7 版本的 Windows 驱动程序工具包中已过时，在将来的 WDK 版本中可能不受支持。

 

本主题提供了从命令行使用 BinPlace 的示例。

首先，可以设置根目标目录，如下所示：

```
set _NTTREE=d:\ProjectRoot
```

然后，可以按以下方式设置位置文件的路径和文件名：

```
set BINPLACE_PLACEFILE=d:\mystuff\myplacefile.txt
```

让文件 d： mystuffmyplacefile.txt 的内容 \\ 如下所示 \\ ：

```
; This is a simple place file.
commonmodule.dll   retail
application.exe    files\bin
mydriver.sys       *\drivertree
extra.cab          appendix
```

现在，可以通过以下命令运行 BinPlace：

```
binplace g:\somelocation\extra.cab
```

由于 extra.cab 不是可执行文件，BinPlace 将仅移动它。 根目标目录为 d： \\ projectroot。 此文件的类目录是在 "将文件放入" **附录** 中指定的。 文件类型子目录为 cab (要移动) 文件的文件扩展名。 因此，会将此文件复制到位置 d： \\ projectroot \\ 附录 \\ cab \\extra.cab。

现在对可执行文件及其符号文件使用 BinPlace。 为此，请指定可执行文件的名称--BinPlace 将找到关联的符号文件。

将可执行文件的名称传递到 BinPlace 时，它会在与可执行文件相同的目录中查找其符号文件。 如果找不到，它将读取存储在可执行文件中的 CodeView 记录;如果它在该记录中找到符号文件路径，则将在该路径中查找符号文件。

**注意**   如果显式指定符号文件名，BinPlace 只会移动它，而不会对其进行处理。

 

```
binplace -a -x -s d:\stripped -n g:\full g:\builddir\application.exe
```

可执行文件使用与之前相同的根目标目录。 其类目录是 "文件" \\ bin。 因此，它位于 d： \\ projectroot \\ files \\ binapplication.exe 中 \\ 。

符号文件放置在两个位置。 完整的符号文件 (包含私有和公共符号) 转到 g： \\ 完整 \\ 文件 \\ bin \\ exe \\ 应用程序 .pdb。 去除的符号文件 (仅包含公共符号) 转到 d：已 \\ 去除的 \\ 文件 \\ bin \\ exe \\ 应用程序 .pdb。

现在，在 commonmodule.dll 上使用类似的命令：

```
binplace -a -x -s d:\stripped -n g:\full g:\builddir\commonmodule.dll
```

这次，类子目录为 **零售**。 对于可执行文件，此目录名称是 "不使用类子目录" 的代码，因此它位于 d： \\ projectroot \\application.exe 中。 符号文件位于 g： \\ full \\ 零售 \\ dll \\ 应用程序 .pdb 和 d：已 \\ 去除 \\ 零售 \\ dll .pdb 中 \\ 。

最后，在 mydriver.sys 上使用 BinPlace 并省略 **-n** 开关：

```
binplace -a -x -s d:\stripped g:\builddir\mydriver.sys
```

此类子目录为 **\* /drivertree**。 对于可执行文件，星号 (\*) 替换为处理器类型。 假设你在 x86 计算机上运行，可执行文件位于 d： \\ projectroot \\ i386 \\ drivertree \\application.exe 中。 \\ \\ \\ \\ 由于符号文件的星号被忽略，因此去除的符号文件位于 g： full drivertree sys 应用程序 .pdb 中。 由于省略了 **-n** 开关，因此不会将完整的符号文件放在任何位置。

 

 






---
title: 将清单文件与 SymChk 配合使用
description: 将清单文件与 SymChk 配合使用
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6867a05e345451abd5669ea932edf61814cb5a55
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803203"
---
# <a name="using-a-manifest-file-with-symchk"></a>将清单文件与 SymChk 配合使用


## <span id="ddk_using_symchk_dtoolq"></span><span id="DDK_USING_SYMCHK_DTOOLQ"></span>


在某些情况下，可能需要检索位于独立计算机上的文件的符号;也就是说，计算机不在任何网络上，或位于没有符号存储的网络上。 在这种情况下，可以使用以下过程来检索符号。

1.  使用 **/om** 参数运行 SymChk，以创建描述要检索其符号的文件的清单文件。

2.  将清单文件移动到具有符号存储区的网络。

3.  运行带有 **/im** 参数的 SymChk，以检索清单文件中所描述文件的符号。

4.  将符号文件移回独立计算机。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

假设 yourApp.exe 在独立的计算机上运行。 下面的命令创建一个清单文件，用于描述调试 yourApp.exe pocess 所需的所有符号。

```dbgcmd
C:\>SymChk /om c:\Manifest\man.txt /ie yourApp.exe

SYMCHK: FAILED files = 0
SYMCHK: PASSED + IGNORED files = 28
```

现在假设已将清单文件移动到可访问符号存储区的网络上的另一台计算机。 下面的命令检索清单文件中描述的符号，并将其放在 mySymbols 文件夹中。

```dbgcmd
C:\>SymChk /im c:\FolderOnOtherComputer\man.txt /s srv*c:\mysymbols*\\aServer\symbols

SYMCHK: myApp.exe             ERROR - Unable to download file. Error reported was 2
. . .
SYMCHK: FAILED files = 28
SYMCHK: PASSED + IGNORED files = 28
```

现在，你可以将符号移到隔离的计算机并将其用于调试。

 

 






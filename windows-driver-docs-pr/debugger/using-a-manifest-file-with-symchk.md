---
title: 将清单文件与 SymChk 配合使用
description: 将清单文件与 SymChk 配合使用
ms.assetid: ee5d0c39-1838-4595-adf4-6cd1261a57c8
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7db76f75ecab5769c2ce33554f3c5500b247fdc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367969"
---
# <a name="using-a-manifest-file-with-symchk"></a>将清单文件与 SymChk 配合使用


## <span id="ddk_using_symchk_dtoolq"></span><span id="DDK_USING_SYMCHK_DTOOLQ"></span>


在某些情况下，您可能需要检索位于独立的计算机; 的文件的符号即，计算机不在任何网络上或位于具有无符号存储区的网络。 在这种情况下，可以使用以下过程来检索的符号。

1.  运行与 SymChk **/om**参数来创建描述您想要检索的符号的文件的清单文件。

2.  将清单文件移动到具有符号存储区的网络。

3.  运行与 SymChk **/im**参数，检索在清单文件中所述的文件的符号。

4.  将符号文件移回的独立计算机。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

假设 yourApp.exe 独立计算机上运行。 以下命令创建描述调试 yourApp.exe pocess 所需的所有符号的清单文件。

```dbgcmd
C:\>SymChk /om c:\Manifest\man.txt /ie yourApp.exe

SYMCHK: FAILED files = 0
SYMCHK: PASSED + IGNORED files = 28
```

现在假定您已移到符号存储区中有权访问的网络上的其他计算机的清单文件。 以下命令检索在清单文件中所述的符号，并将其置于 mySymbols 文件夹中。

```dbgcmd
C:\>SymChk /im c:\FolderOnOtherComputer\man.txt /s srv*c:\mysymbols*\\aServer\symbols

SYMCHK: myApp.exe             ERROR - Unable to download file. Error reported was 2
. . .
SYMCHK: FAILED files = 28
SYMCHK: PASSED + IGNORED files = 28
```

现在可以将这些符号移动到独立的计算机，并将它们用于调试。

 

 






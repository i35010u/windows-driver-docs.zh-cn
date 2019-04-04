---
title: CTRL+W（显示调试器版本）
description: CTRL + W 键显示调试程序和所有已加载的扩展 Dll 的版本信息。
ms.assetid: 9651965e-fbf5-4084-adcd-63de60998b8b
keywords:
- CTRL + W （显示调试器版本） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+W (Show Debugger Version)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6d70f693c518b594259c9d4cb1d15ffd50091977
ms.sourcegitcommit: 672bf3fd18f6c169b5634476613ce1da9250413b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/03/2019
ms.locfileid: "58898058"
---
# <a name="ctrlw-show-debugger-version"></a>CTRL+W（显示调试器版本）


CTRL + W 键显示调试程序和所有已加载的扩展 Dll 的版本信息。

CDB / KD 语法

```dbgcmd
CTRL+W  ENTER 
```

WinDbg 语法

```dbgcmd
CTRL+ALT+W 
```


## <a name="environment"></a>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>调试程序</strong></p></td>
<td align="left"><p>KD、 CDB WinDbg</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

这具有相同的效果[**版本 （显示调试器版本）** ](version--show-debugger-version-.md)命令，只不过后一种命令显示 Windows 操作系统版本。

在 WinDbg 中，还可以通过选择[视图 |显示版本](view---show-version.md)。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**version（显示调试器版本）**](version--show-debugger-version-.md)

[**vertarget（显示目标计算机版本）**](vertarget--show-target-computer-version-.md)

 

 







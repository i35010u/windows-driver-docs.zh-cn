---
title: CTRL+W（显示调试器版本）
description: CTRL + W 键显示调试器和所有加载的扩展 Dll 的版本信息。
keywords:
- CTRL + W (显示调试器版本) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+W (Show Debugger Version)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e33f037c287b173e388f52af9eda9b69d6c65ed1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786973"
---
# <a name="ctrlw-show-debugger-version"></a>CTRL+W（显示调试器版本）


CTRL + W 键显示调试器和所有加载的扩展 Dll 的版本信息。

CDB/KD 语法

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
<td align="left"><p><strong>调试器</strong></p></td>
<td align="left"><p>CDB、KD、WinDbg</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

这与 [**版本 (Show 调试器版本)**](version--show-debugger-version-.md) 命令相同，不同之处在于后一命令显示 Windows 操作系统版本。

在 WinDbg，还可以通过选择 "视图" [| "显示版本](view---show-version.md)。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**version（显示调试器版本）**](version--show-debugger-version-.md)

[**vertarget（显示目标计算机版本）**](vertarget--show-target-computer-version-.md)

 

 







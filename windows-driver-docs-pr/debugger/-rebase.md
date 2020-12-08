---
title: 变基
description: 变基扩展在文件中搜索指定地址或符号。
keywords:
- 变基 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rebase
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: adaffec2c8f5b75760341ad29b93d3b6e74d23ff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815495"
---
# <a name="rebase"></a>!rebase


**！变基** 扩展在文件中搜索指定地址或符号的文件。

```dbgcmd
!rebase [-r] Address [Path]
!rebase Symbol [Path]
!rebase -stack [Path]
!rebase -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-r______"></span><span id="_______-R______"></span>**-r**   
尝试加载在变基. 日志中找到的任何模块。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定标准十六进制格式的地址。 该扩展将搜索此地址附近的 Dll。

<span id="_______Path______"></span><span id="_______path______"></span><span id="_______PATH______"></span>*路径*   
指定变基的文件路径。 如果未指定 *路径* ，则该扩展将尝试猜测变基的路径。日志或失败，尝试从当前工作目录读取一个变基文件。

<span id="_______Symbol______"></span><span id="_______symbol______"></span><span id="_______SYMBOL______"></span>*符号*   
指定符号或图像名称。 该扩展将搜索包含此子字符串的 Dll。

<span id="_______-stack______"></span><span id="_______-STACK______"></span>**-stack**   
显示当前堆栈中的所有模块。

<span id="_______-_______"></span> **-?**   
在调试器中显示此扩展的简短帮助文本命令窗口。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

 

 






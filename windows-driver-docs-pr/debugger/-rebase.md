---
title: 重定基本值
description: 重定基本值扩展搜索 rebase.log 文件中指定的地址或符号。
ms.assetid: 811e7ab8-301f-433a-bfc4-8a4e5f002b30
keywords:
- 重定基本值 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rebase
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 66c00390ea06a189b8f6541cfac89cfcd65ec34b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547547"
---
# <a name="rebase"></a>！ 重定基本值


**！ 重定基本值**扩展搜索 rebase.log 文件中指定的地址或符号。

```dbgcmd
!rebase [-r] Address [Path]
!rebase Symbol [Path]
!rebase -stack [Path]
!rebase -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-r______"></span><span id="_______-R______"></span> **-r**   
尝试加载在 rebase.log 中找到任何模块。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
在标准十六进制格式中指定的地址。 该扩展将此地址附近搜索 Dll。

<span id="_______Path______"></span><span id="_______path______"></span><span id="_______PATH______"></span> *路径*   
指定 rebase.log 的文件路径。 如果*路径*中未指定，则尝试猜测的路径 rebase.log，或如果没有问题，该扩展，尝试从当前工作目录中读取 rebase.log 文件。

<span id="_______Symbol______"></span><span id="_______symbol______"></span><span id="_______SYMBOL______"></span> *符号*   
指定符号或图像名称。 该扩展将搜索包含此子字符串的 Dll。

<span id="_______-stack______"></span><span id="_______-STACK______"></span> **-stack**   
显示当前堆栈中的所有模块。

<span id="_______-_______"></span> **-?**   
在调试器命令窗口中显示此扩展的简短帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

 

 






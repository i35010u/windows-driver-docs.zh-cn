---
title: bitcount
description: ！ Bitcount 扩展对内存范围内的"1"比特数进行计数。
ms.assetid: dacf3d63-6241-4779-afca-514905b37e26
keywords:
- bitcount Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bitcount
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e5b05f50dd6941ae1fc1ffee34db45a4cdeb5789
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334694"
---
# <a name="bitcount"></a>!bitcount


**！ Bitcount**扩展对内存范围内的"1"比特数进行计数。

```dbgcmd
!bitcount StartAddress TotalBits
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
指定其"1"的位将被计算在内的内存范围的起始地址。

<span id="_______TotalBits______"></span><span id="_______totalbits______"></span><span id="_______TOTALBITS______"></span> *TotalBits*   
以位为单位指定内存范围的大小。

<span id="_______-_______"></span> **-?**   
显示此扩展中的一些帮助文本[调试器命令窗口](debugger-command-window.md)。

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
<td align="left"><p>Exts.dll</p></td>
</tr>
</tbody>
</table>

 

 

 






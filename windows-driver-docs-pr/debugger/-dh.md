---
title: dh
description: Dh 扩展显示指定图像的标头。
ms.assetid: 1b4f94ae-42cc-4381-a2d1-c2f248e4d5a6
keywords:
- NTFS 文件对象
- dh Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dh
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 409da4bb352fd554c6775a9e9a72b906c19de5f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577103"
---
# <a name="dh"></a>!dh


**！ Dh**扩展显示指定图像的标头。

```dbgcmd
!dh [Options] Address 
!dh -h
```

## <a name="span-idddkdhdbgspanspan-idddkdhdbgspanparameters"></a><span id="ddk__dh_dbg"></span><span id="DDK__DH_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
以下选项之一：

<span id="-f"></span><span id="-F"></span>**-f**  
显示文件标头。

<span id="-s"></span><span id="-S"></span>**-s**  
显示部分标头。

<span id="-a"></span><span id="-A"></span>**-a**  
显示所有标头信息。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定图像的十六进制的地址。

<span id="_______-h______"></span><span id="_______-H______"></span> **-h**   
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
<td align="left"><p></p>
Dbghelp.dll Kdextx86.dll Ntsdexts.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Dbghelp.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

[ **！ Lmi** ](-lmi.md)扩展从映像标头中提取最重要的信息并将其显示摘要以简洁格式。 该扩展是比通常更有用 **！ dh**。

 

 






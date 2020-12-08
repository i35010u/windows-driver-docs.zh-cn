---
title: dh
description: Dh 扩展显示指定映像的标头。
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
ms.openlocfilehash: 7852f9187a148fb5dd9e03638f267c2bb6837322
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805899"
---
# <a name="dh"></a>!dh


**！ Dh** 扩展显示指定映像的标头。

```dbgcmd
!dh [Options] Address 
!dh -h
```

## <a name="span-idddk__dh_dbgspanspan-idddk__dh_dbgspanparameters"></a><span id="ddk__dh_dbg"></span><span id="DDK__DH_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
以下选项之一：

<span id="-f"></span><span id="-F"></span>**-f**  
显示文件头。

<span id="-s"></span><span id="-S"></span>**-s**  
显示节标头。

<span id="-a"></span><span id="-A"></span>**-a**  
显示所有标头信息。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定图像的十六进制地址。

<span id="_______-h______"></span><span id="_______-H______"></span>**-h**   
在 [调试器命令窗口](debugger-command-window.md)中显示此扩展的一些帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

[**！ Lmi**](-lmi.md) extension 从图像标头提取最重要的信息，并以简洁的摘要格式显示它。 该扩展通常比 **！ dh** 更有用。

 

 






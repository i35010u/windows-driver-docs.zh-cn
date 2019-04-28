---
title: minipkd.help
description: Minipkd.help 扩展显示 Minipkd.dll 扩展命令的帮助文本。
ms.assetid: 5629aec8-8c9d-4ed0-91fb-c8d020f78405
keywords:
- minipkd.help Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- minipkd.help
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 005fb48ab498aafad1f79b443d68bf37118ce51c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336076"
---
# <a name="minipkdhelp"></a>!minipkd.help


**！ Minipkd.help**扩展显示 Minipkd.dll 扩展命令的帮助文本。

```dbgcmd
!minipkd.help 
```

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
<td align="left"><p>Minipkd.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[SCSI 微型端口调试](scsi-miniport-debugging.md)。

<a name="remarks"></a>备注
-------

如果出现类似于以下错误消息，它指示符号路径不正确，并且不指向 Scsiport.sys 符号的正确版本。

```dbgcmd
minipkd error (0) <path> ... \minipkd\minipkd.c @ line 435
```

使用[ **.sympath （设置符号路径）** ](-sympath--set-symbol-path-.md)命令显示当前路径，并将路径更改。 使用[ **.reload （重新加载模块）** ](-reload--reload-module-.md)命令以重新加载当前路径中的符号。

 

 






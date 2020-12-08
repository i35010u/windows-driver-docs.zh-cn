---
title: minipkd。帮助
description: Minipkd 扩展显示 Minipkd.dll 扩展命令的帮助文本。
keywords:
- minipkd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- minipkd.help
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9ba253156b8a159f1385664e2b380e2e66abcc9e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798423"
---
# <a name="minipkdhelp"></a>!minipkd.help


**！ Minipkd** 显示 Minipkd.dll 扩展命令的帮助文本。

```dbgcmd
!minipkd.help 
```

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
<td align="left"><p>Minipkd.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [SCSI 微型端口调试](scsi-miniport-debugging.md)。

<a name="remarks"></a>备注
-------

如果出现类似于下面的错误消息，则表示符号路径不正确，并且不指向正确的 Scsiport.sys 符号版本。

```dbgcmd
minipkd error (0) <path> ... \minipkd\minipkd.c @ line 435
```

使用 [**. sympath (设置符号路径)**](-sympath--set-symbol-path-.md) 命令来显示当前路径并更改路径。 使用 [**. reload.sql (Reload.sql Module)**](-reload--reload-module-.md) 命令从当前路径重新加载符号。

 

 






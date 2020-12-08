---
title: rpcexts.eerecord
description: Rpcexts. eerecord 扩展显示扩展错误信息记录的内容。
keywords:
- rpcexts eerecord Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.eerecord
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bf7bb346f660de483cc43064120dada751a0b5a5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817881"
---
# <a name="rpcextseerecord"></a>!rpcexts.eerecord


**！ Rpcexts eerecord** 扩展显示扩展错误信息记录的内容。

```dbgcmd
!rpcexts.eerecord EERecordAddress
```

## <a name="span-idddk__rpcexts_eerecord_dbgspanspan-idddk__rpcexts_eerecord_dbgspanparameters"></a><span id="ddk__rpcexts_eerecord_dbg"></span><span id="DDK__RPCEXTS_EERECORD_DBG"></span>参数


<span id="_______EERecordAddress______"></span><span id="_______eerecordaddress______"></span><span id="_______EERECORDADDRESS______"></span>*EERecordAddress*   
指定扩展错误记录的地址。

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
<td align="left"><p>Rpcexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关调试 Microsoft 远程过程调用 (RPC) 的详细信息，请参阅 [Rpc 调试](rpc-debugging.md)。

<a name="remarks"></a>备注
-------

此扩展在调试器中显示一个扩展错误信息记录的内容。 在大多数情况下，更易于使用 [**！ rpcexts**](-rpcexts-eeinfo.md)，后者显示整个链。 如果链非常长并且只希望看到一条记录，请使用 **！ eerecord** 。

以下是示例：

```dbgcmd
0:001> !rpcexts.eerecord 0xb015f0
Computer Name: (null)
ProcessID: 708 (0x2C4)
System Time is: 3/21/2000 4:3:0:264
Generating component: 8
Status: 14
Detection Location: 311
Flags:
Parameter 0:(Long value) : -30976 (0xFFFF8700)
Parameter 1:(Long value) : 16777343 (0x100007F)
```

 

 






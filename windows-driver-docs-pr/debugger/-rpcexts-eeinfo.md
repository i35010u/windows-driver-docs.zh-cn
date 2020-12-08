---
title: rpcexts.eeinfo
description: Rpcexts. eeinfo 扩展显示扩展的错误消息链。
keywords:
- rpcexts eeinfo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.eeinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 421a58838c598d0101ab1e4224c4077aee7a143f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790087"
---
# <a name="rpcextseeinfo"></a>!rpcexts.eeinfo


**！ Rpcexts eeinfo** 扩展显示扩展的错误消息链。

```dbgcmd
!rpcexts.eeinfo EEInfoAddress
```

## <a name="span-idddk__rpcexts_eeinfo_dbgspanspan-idddk__rpcexts_eeinfo_dbgspanparameters"></a><span id="ddk__rpcexts_eeinfo_dbg"></span><span id="DDK__RPCEXTS_EEINFO_DBG"></span>参数


<span id="_______EEInfoAddress______"></span><span id="_______eeinfoaddress______"></span><span id="_______EEINFOADDRESS______"></span>*EEInfoAddress*   
指定扩展错误信息的地址。

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

此扩展显示扩展错误消息链中所有记录的内容。

记录按顺序显示，最新记录首先显示。 记录由虚线分隔。

下面是一个示例 (，其中只有一条记录) ：

```dbgcmd
0:001> !rpcexts.eeinfo 0xb015f0
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

如果链非常长并且只希望看到一条记录，请改用 [**！ rpcexts. eerecord**](-rpcexts-eerecord.md) 。

 

 






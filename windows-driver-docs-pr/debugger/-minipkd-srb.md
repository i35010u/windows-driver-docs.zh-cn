---
title: minipkd.srb
description: Minipkd. srb 扩展显示 (SRB) 数据结构的指定 SCSI 请求块。
keywords:
- minipkd srb Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- minipkd.srb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c8932dd73eeab6460b2a9e9e3b7f050adf7a1885
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798411"
---
# <a name="minipkdsrb"></a>!minipkd.srb


**！ Minipkd srb** (srb) 数据结构中显示指定的 SCSI 请求块。

```dbgcmd
!minipkd.srb SRB 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______SRB______"></span><span id="_______srb______"></span>*SRB*   
指定 SRB 的地址。

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

可以在 [**！ minipkd**](-minipkd-req.md)命令的输出的 *SRB* 字段中找到所有当前活动的请求的地址。

此扩展显示 SRB、其寻址的驱动程序、发出 SRB 的 SCSI 和其地址以及十六进制标志值的状态。 如果在 "标志" 值中设置了0x10000，则此请求当前在微型端口中。

 

 






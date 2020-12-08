---
title: minipkd.portconfig
description: Minipkd. portconfig 扩展显示有关指定 PORT_CONFIGURATION_INFORMATION 数据结构的信息。
keywords:
- minipkd portconfig Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- minipkd.portconfig
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b893ea1cdc9606903137397cc31005a05d5fef10
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798417"
---
# <a name="minipkdportconfig"></a>!minipkd.portconfig


**！ Minipkd. portconfig** 扩展显示有关指定端口 \_ 配置 \_ 信息数据结构的信息。

```dbgcmd
!minipkd.portconfig PortConfig 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______PortConfig______"></span><span id="_______portconfig______"></span><span id="_______PORTCONFIG______"></span>*PortConfig*   
指定端口 \_ 配置 \_ 信息数据结构的地址。

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

可以在 [**！ minipkd**](-minipkd-adapter.md)显示的 "**端口配置信息**" 字段中找到 *PortConfig* 地址。

 

 






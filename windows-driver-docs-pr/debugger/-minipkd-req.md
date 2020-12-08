---
title: minipkd
description: Minipkd 扩展显示有关指定适配器或设备上所有当前活动的请求的信息。
keywords:
- minipkd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- minipkd.req
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b53b8064431c614c589b2a11837ea9351b1e49cd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798413"
---
# <a name="minipkdreq"></a>!minipkd.req


**！ Minipkd** 扩展显示有关指定适配器或设备上所有当前活动的请求的信息。

```dbgcmd
!minipkd.req Adapter 
!minipkd.req Device 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Adapter______"></span><span id="_______adapter______"></span><span id="_______ADAPTER______"></span>*适配器*   
指定适配器的地址。

<span id="_______Device______"></span><span id="_______device______"></span><span id="_______DEVICE______"></span>*设备*   
为逻辑单元扩展 (LUN) 设备指定 (PDO) 的物理设备对象。

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

可以在 [**！ minipkd**](-minipkd-adapters.md)显示的 " **DevObj** " 字段中找到 LUN 的 PDO。

 

 






---
title: isainfo
description: Isainfo 扩展显示有关 PNPISA 卡或系统中存在的设备的信息。
keywords:
- I/o 总线
- CARD_INFORMATION
- isainfo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- isainfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 318f2b06c46d08e18656346e92d8cbff83d1782f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786493"
---
# <a name="isainfo"></a>!isainfo


**！ Isainfo** extension 显示有关 PNPISA 卡或系统中存在的设备的信息。

```dbgcmd
!isainfo [Card]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Card______"></span><span id="_______card______"></span><span id="_______CARD______"></span>*卡*   
指定 PNPISA 卡。 如果 *卡* 为0或省略，则 PNPISA 上的所有设备和卡 (即，将显示 PC I/o) 总线。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

下面是此扩展的输出示例：

```dbgcmd
0: kd> !isainfo
ISA PnP FDO @ 0x867b9938, DevExt @ 0x867b99f0, Bus # 0
Flags (0x80000000)  DF_BUS

  ISA PnP PDO @ 0x867B9818, DevExt @ 0x86595388
  Flags (0x40000818)  DF_ENUMERATED, DF_ACTIVATED, 
                      DF_REQ_TRIMMED, DF_READ_DATA_PORT
```

 

 






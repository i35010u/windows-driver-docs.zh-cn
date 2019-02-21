---
title: isainfo
description: Isainfo 扩展显示 PNPISA 卡信息或在系统中存在的设备...
ms.assetid: 8caa501e-3bb7-4af8-a7ea-e8b255b9f24c
keywords:
- I/O 总线
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
ms.openlocfilehash: ae347aa0f24202db04c121fe40094255c85d6d8b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543462"
---
# <a name="isainfo"></a>！ isainfo


**！ Isainfo**扩展显示 PNPISA 卡信息或在系统中存在的设备...

```dbgcmd
!isainfo [Card]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Card______"></span><span id="_______card______"></span><span id="_______CARD______"></span> *Card*   
指定 PNPISA 卡。 如果*卡*为 0 或省略，所有设备和 PNPISA (即，PC I/O) 总线上的卡会都显示。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

下面是输出的来自此扩展插件示例：

```dbgcmd
0: kd> !isainfo
ISA PnP FDO @ 0x867b9938, DevExt @ 0x867b99f0, Bus # 0
Flags (0x80000000)  DF_BUS

  ISA PnP PDO @ 0x867B9818, DevExt @ 0x86595388
  Flags (0x40000818)  DF_ENUMERATED, DF_ACTIVATED, 
                      DF_REQ_TRIMMED, DF_READ_DATA_PORT
```

 

 






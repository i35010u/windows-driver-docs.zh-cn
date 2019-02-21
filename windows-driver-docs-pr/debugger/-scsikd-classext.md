---
title: scsikd.classext
description: Scsikd.classext 扩展显示指定的类插 (PnP) 设备。
ms.assetid: 2b56966c-7ae1-4d44-ad60-19f31e47efff
keywords:
- scsikd.classext Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- scsikd.classext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f96bc8d523df3f04e3bbf1905ed5576c2fdc6ae4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547436"
---
# <a name="scsikdclassext"></a>!scsikd.classext


**！ Scsikd.classext**扩展将显示指定的类插即用 (PnP) 设备。

```dbgcmd
!scsikd.classext [Device [Level]] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Device______"></span><span id="_______device______"></span><span id="_______DEVICE______"></span> *设备*   
指定的设备对象或类即插即用设备的设备扩展。 如果*设备*是省略，将显示所有类即插即用扩展的列表。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *级别*   
指定要显示的详细信息。 此参数可以采用 0、 1 或 2 作为值，2 提供的大部分详细信息。 默认值为 0。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Scsikd.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Scsikd.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[SCSI 微型端口调试](scsi-miniport-debugging.md)。

<a name="remarks"></a>备注
-------

下面是举例 **！ scsikd.classext**显示：

```dbgcmd
0: kd> !scsikd.classext
  ' !scsikd.classext 8633e3f0 '   (             ) "IBM     " / "DDYS-T09170M    " / "S93E" / "        XBY45906"
  ' !scsikd.classext 86347b48 '   (paging device) "IBM     " / "DDYS-T09170M    " / "S80D" / "        VDA60491"
  ' !scsikd.classext 86347360 '   (             ) "UNISYS  " / "003451ST34573WC " / "5786" / "HN0220750000181300L6"
  ' !scsikd.classext 861d1898 '   (             ) "" / "MATSHITA CD-ROM CR-177" / "7T03" / ""

 usage: !classext <class fdo> <level [0-2]> 
```

 

 






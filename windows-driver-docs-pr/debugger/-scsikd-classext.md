---
title: scsikd.classext
description: Classext 扩展即插即用 (PnP) 设备中显示指定的类。
keywords:
- scsikd classext Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- scsikd.classext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1d7afb7a56c903c4fe990799e63b49eca134f3be
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837575"
---
# <a name="scsikdclassext"></a>!scsikd.classext


**！ Scsikd classext** 即插即用 (PnP) 设备中显示指定的类。

```dbgcmd
!scsikd.classext [Device [Level]] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Device______"></span><span id="_______device______"></span><span id="_______DEVICE______"></span>*设备*   
指定类 PnP 设备的设备对象或设备扩展。 如果省略 *设备* ，则显示所有类 PnP 扩展的列表。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span>*级别*   
指定要显示的详细信息的数量。 此参数的值可以是0、1或2，其中2提供最详细的信息。 默认值为 0。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [SCSI 微型端口调试](scsi-miniport-debugging.md)。

<a name="remarks"></a>备注
-------

下面是 **！ classext** 显示的示例 scsikd：

```dbgcmd
0: kd> !scsikd.classext
  ' !scsikd.classext 8633e3f0 '   (             ) "IBM     " / "DDYS-T09170M    " / "S93E" / "        XBY45906"
  ' !scsikd.classext 86347b48 '   (paging device) "IBM     " / "DDYS-T09170M    " / "S80D" / "        VDA60491"
  ' !scsikd.classext 86347360 '   (             ) "UNISYS  " / "003451ST34573WC " / "5786" / "HN0220750000181300L6"
  ' !scsikd.classext 861d1898 '   (             ) "" / "MATSHITA CD-ROM CR-177" / "7T03" / ""

 usage: !classext <class fdo> <level [0-2]> 
```

 

 






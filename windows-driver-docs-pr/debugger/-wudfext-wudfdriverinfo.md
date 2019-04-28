---
title: wudfext.wudfdriverinfo
description: Wudfext.wudfdriverinfo 扩展显示有关当前的主机进程内 UMDF 驱动程序的信息。
ms.assetid: 6204df00-2de5-41b6-80c1-ba576699fb20
keywords:
- wudfext.wudfdriverinfo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfdriverinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 42f87e0977ffec834ed692d9f485ce616379d4d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349101"
---
# <a name="wudfextwudfdriverinfo"></a>!wudfext.wudfdriverinfo


**！ Wudfext.wudfdriverinfo**扩展显示有关当前的主机进程内 UMDF 驱动程序的信息。

```dbgcmd
!wudfext.wudfdriverinfo Name
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span> *名称*   
指定要显示有关的信息的 UMDF 驱动程序的名称。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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
<td align="left"><p>Wudfext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

**！ Wudfext.wudfdriverinfo**扩展循环访问每个设备堆栈中每个级别，并显示每个条目相匹配的驱动程序中指定其名称的驱动程序和设备信息*名称*参数。

可以使用 **！ wudfext.wudfdriverinfo**快速查找您的驱动程序的设备对象。

以下是一种 **！ wudfext.wudfdriverinfo**显示：

```dbgcmd
kd> !wudfdriverinfo wudfechodriver 
IWDFDriver: 0xf2db8
  !WDFDEVICE 0xf2f80
    !devstack 0x34e4e0 @ level 0
```

 

 






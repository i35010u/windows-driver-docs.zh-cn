---
title: wudfext.wudfdriverinfo
description: Wudfext. wudfdriverinfo 扩展显示有关当前主机进程内的 UMDF 驱动程序的信息。
keywords:
- wudfext wudfdriverinfo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfdriverinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 34c3cdb555af2852687fd0b63bf7977e069a834e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794067"
---
# <a name="wudfextwudfdriverinfo"></a>!wudfext.wudfdriverinfo


**！ Wudfext wudfdriverinfo** 扩展显示有关当前主机进程内的 UMDF 驱动程序的信息。

```dbgcmd
!wudfext.wudfdriverinfo Name
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span>*名称*   
指定要显示其相关信息的 UMDF 驱动程序的名称。

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
<td align="left"><p>Wudfext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

**！ Wudfext wudfdriverinfo** 扩展会遍历每个设备堆栈中的每个级别，并显示与该驱动程序的驱动程序和设备信息匹配的每个条目，该驱动程序的名称是在 *name* 参数中指定的。

可以使用 **！ wudfext** 快速查找驱动程序的设备对象。

下面是 **！ wudfext** 显示的示例：

```dbgcmd
kd> !wudfdriverinfo wudfechodriver 
IWDFDriver: 0xf2db8
  !WDFDEVICE 0xf2f80
    !devstack 0x34e4e0 @ level 0
```

 

 






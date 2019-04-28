---
title: wudfext.umdevstack
description: Wudfext.umdevstack 扩展的主机进程中显示有关设备堆栈的详细的信息。
ms.assetid: 3cce0e30-ea04-4587-9208-b6a7d51fd44a
keywords:
- wudfext.umdevstack Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.umdevstack
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d0b715e70d69a55e28dc47160ca9a1d3ea7e1262
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347961"
---
# <a name="wudfextumdevstack"></a>!wudfext.umdevstack


**！ Wudfext.umdevstack**扩展的主机进程中显示有关设备堆栈详细的信息。

```dbgcmd
!wudfext.umdevstack DevstackAddress [Flags] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______DevstackAddress______"></span><span id="_______devstackaddress______"></span><span id="_______DEVSTACKADDRESS______"></span> *DevstackAddress*   
指定要显示有关的信息的设备堆栈的地址。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 指定要显示的信息的类型。 *标志*可以是以下位的任意组合。 默认值为 0x01。

<span id="Bit_0__0x01_"></span><span id="bit_0__0x01_"></span><span id="BIT_0__0X01_"></span>位 0 (0x01)  
显示有关设备堆栈的详细的信息。

<span id="Bit_8__0x80_"></span><span id="bit_8__0x80_"></span><span id="BIT_8__0X80_"></span>8 位 (0x80)  
显示内部框架有关的信息。

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

 

### <a name="span-idadditionalinformation1spanspan-idadditionalinformation1spanadditional-information"></a><span id="additional_information1"></span><span id="ADDITIONAL_INFORMATION1"></span>其他信息

有关详细信息，请参阅[用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

以下是一种 **！ wudfext.umdevstack**显示：

```dbgcmd
kd> !umdevstack 0x0034e4e0
Device Stack: 0x0034e4e0  Pdo Name: \Device\00000057
 Number of UM drivers: 0x1
  Driver 00:
    Driver Config Registry Path: WUDFEchoDriver
    UMDriver Image Path: C:\Windows\system32\DRIVERS\UMDF\WUDFEchoDriver.dll
    Fx Driver: IWDFDriver 0xf2db8
    Fx Device: IWDFDevice 0xf2f80
        IDriverEntry: WUDFEchoDriver!CMyDriver 0x000f2c70
```

 

 






---
title: ecb，ecd ecw
description: Ecb、 ecd 和 ecw 扩展写入 PCI 配置空间。
ms.assetid: ab5f5164-7666-48ac-aeba-5f238c2625f6
keywords:
- ecb，ecd，ecw Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ecb, ecd, ecw
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 07fb432e992f16690b2bdc9ab70914bd32f9f355
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336866"
---
# <a name="ecb-ecd-ecw"></a>!ecb、!ecd、!ecw


**！ Ecb**， **！ ecd**，并 **！ ecw**扩展写入 PCI 配置空间。

```dbgcmd
!ec Bus.Device.Function Offset Data 
```

## <a name="span-idddkecdbgspanspan-idddkecdbgspanparameters"></a><span id="ddk__ec__dbg"></span><span id="DDK__EC__DBG"></span>参数


<span id="_______Bus______"></span><span id="_______bus______"></span><span id="_______BUS______"></span> *总线*   
指定在总线。 *总线*范围可以介于 0 到 0xFF。

<span id="_______Device______"></span><span id="_______device______"></span><span id="_______DEVICE______"></span> *设备*   
指定设备的插槽设备号。

<span id="_______Function______"></span><span id="_______function______"></span><span id="_______FUNCTION______"></span> *函数*   
指定设备的插槽函数号。

<span id="_______Offset______"></span><span id="_______offset______"></span><span id="_______OFFSET______"></span> *Offset*   
指定要写入的地址。

<span id="_______Data______"></span><span id="_______data______"></span><span id="_______DATA______"></span> *数据*   
指定要写入的值。 有关 **！ ecb**扩展名*数据*必须是 1 个字节 （两个十六进制数字）。 有关 **！ ecw**扩展名*数据*必须是一个单词 （四个十六进制数字）。 有关 **！ ecd**扩展名*数据*必须是一个 DWORD （八个十六进制数字）。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kext.dll</p></td>
</tr>
</tbody>
</table>

 

这些扩展命令仅用于基于 x86 的目标计算机。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

请参阅[插调试](plug-and-play-debugging.md)对于此扩展命令，以及一些其他示例的应用程序。 有关 PCI 总线的信息，请参阅 Windows Driver Kit (WDK) 文档。

<a name="remarks"></a>备注
-------

不能使用这些扩展命令编写一系列*数据*值。 这仅可以通过重复使用此扩展。

若要显示的 PCI 配置空间，请使用[ **！ pci 100**](-pci.md)*总线设备函数*。

 

 






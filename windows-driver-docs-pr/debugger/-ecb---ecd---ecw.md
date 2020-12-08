---
title: ecb、ecd、ecw
description: Ecb、ecd 和 ecw 扩展会写入 PCI 配置空间。
keywords:
- ecb、ecd、ecw Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ecb, ecd, ecw
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 674bb0f5a1bfee0e49c78e4a22b106f6b57e8fed
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799877"
---
# <a name="ecb-ecd-ecw"></a>!ecb、!ecd、!ecw


**！ Ecb**， **！ ecd**， **！ ecw** extension 写入 PCI 配置空间。

```dbgcmd
!ec Bus.Device.Function Offset Data 
```

## <a name="span-idddk__ec__dbgspanspan-idddk__ec__dbgspanparameters"></a><span id="ddk__ec__dbg"></span><span id="DDK__EC__DBG"></span>参数


<span id="_______Bus______"></span><span id="_______bus______"></span><span id="_______BUS______"></span>*总线*   
指定总线。 *总线* 的范围为0到0xff。

<span id="_______Device______"></span><span id="_______device______"></span><span id="_______DEVICE______"></span>*设备*   
指定设备的槽设备号。

<span id="_______Function______"></span><span id="_______function______"></span><span id="_______FUNCTION______"></span>*函数*   
指定设备的槽功能号。

<span id="_______Offset______"></span><span id="_______offset______"></span><span id="_______OFFSET______"></span>*偏移量*   
指定要写入的地址。

<span id="_______Data______"></span><span id="_______data______"></span><span id="_______DATA______"></span>*数据*   
指定要写入的值。 对于 **！ ecb** 扩展， *数据* 必须为1个字节 (两个十六进制数字) 。 对于 **！ ecw** Extension， *数据* 必须是一个单词 (四个十六进制数字) 。 对于 **！ ecd** Extension， *数据* 必须是一个 DWORD (8 个十六进制数字) 。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

这些扩展命令只能与基于 x86 的目标计算机一起使用。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

请参阅 [即插即用调试](plug-and-play-debugging.md) 此扩展命令的应用程序，以及一些其他示例。 有关 PCI 总线的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档。

<a name="remarks"></a>备注
-------

不能使用这些扩展命令来写入 *数据* 值序列。 此操作只能通过重复使用此扩展来完成。

若要显示 PCI 配置空间，请使用 [**！ PCI 100**](-pci.md)*总线设备功能*。

 

 






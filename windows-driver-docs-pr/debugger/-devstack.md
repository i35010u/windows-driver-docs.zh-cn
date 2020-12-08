---
title: devstack
description: Devstack 扩展显示与设备对象相关联的设备堆栈的格式化视图。
keywords:
- devstack Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- devstack
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3c7dfc95800ce990e3770f8453ba3dedf8c6410b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805903"
---
# <a name="devstack"></a>!devstack


**！ Devstack** 扩展显示与设备对象相关联的设备堆栈的格式化视图。

```dbgcmd
!devstack DeviceObject 
```

## <a name="span-idddk__devstack_dbgspanspan-idddk__devstack_dbgspanparameters"></a><span id="ddk__devstack_dbg"></span><span id="DDK__DEVSTACK_DBG"></span>参数


<span id="_______DeviceObject______"></span><span id="_______deviceobject______"></span><span id="_______DEVICEOBJECT______"></span>*DeviceObject*   
指定设备对象。 这可以是设备对象结构的十六进制地址 \_ 或设备的名称。

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关设备堆栈的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档。

<a name="remarks"></a>备注
-------

如果 *DeviceObject* 指定设备的名称，但未提供前缀， \\ \\ 则假定为前缀 "device"。 请注意，在使用表达式计算器之前，此命令将检查 *DeviceObject* 是否为有效的地址或设备名称。

以下是示例：

```dbgcmd
kd> !devstack e000000085007b50
 !DevObj   !DrvObj            !DevExt   ObjectName
  e0000165fff32040  \Driver\kmixer     e0000165fff32190  
> e000000085007b50  \Driver\swenum     e000000085007ca0  KSENUM#00000005
!DevNode e0000165fff2e010 :
  DeviceInst is "SW\{b7eafdc0-a680-11d0-96d8-00aa0051e51d}\{9B365890-165F-11D0-A195-0020AFD156E4}"
 ServiceName is "kmixer"
```

 

 






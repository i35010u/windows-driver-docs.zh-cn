---
title: devstack
description: Devstack 扩展显示设备堆栈与设备对象相关联的格式化的视图。
ms.assetid: 2215f166-2053-4525-80cd-be3817510dbd
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
ms.openlocfilehash: 2c00bc4286dfcecf80f497e8ec6c8fa7ef9f28da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543264"
---
# <a name="devstack"></a>！ devstack


**！ Devstack**扩展显示设备堆栈与设备对象相关联的格式化的视图。

```dbgcmd
!devstack DeviceObject 
```

## <a name="span-idddkdevstackdbgspanspan-idddkdevstackdbgspanparameters"></a><span id="ddk__devstack_dbg"></span><span id="DDK__DEVSTACK_DBG"></span>参数


<span id="_______DeviceObject______"></span><span id="_______deviceobject______"></span><span id="_______DEVICEOBJECT______"></span> *DeviceObject*   
指定的设备对象。 这可以是设备的十六进制地址\_对象结构或设备的名称。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关设备堆栈的信息，请参阅 Windows Driver Kit (WDK) 文档。

<a name="remarks"></a>备注
-------

如果*DeviceObject*指定的设备的名称，但提供没有前缀，前缀"\\设备\\"假定。 请注意，此命令将检查以查看是否*DeviceObject*表达式计算器在使用之前为有效的地址或设备名称。

下面是一个示例：

```dbgcmd
kd> !devstack e000000085007b50
 !DevObj   !DrvObj            !DevExt   ObjectName
  e0000165fff32040  \Driver\kmixer     e0000165fff32190  
> e000000085007b50  \Driver\swenum     e000000085007ca0  KSENUM#00000005
!DevNode e0000165fff2e010 :
  DeviceInst is "SW\{b7eafdc0-a680-11d0-96d8-00aa0051e51d}\{9B365890-165F-11D0-A195-0020AFD156E4}"
 ServiceName is "kmixer"
```

 

 






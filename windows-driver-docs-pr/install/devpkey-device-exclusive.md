---
title: DEVPKEY_Device_Exclusive
description: DEVPKEY_Device_Exclusive
ms.assetid: c54c2fe3-cf57-4603-a701-8ddbc28aa47d
keywords:
- DEVPKEY_Device_Exclusive 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_Exclusive
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ffc77d17f5042eaf9070a575df2e432ddf865322
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520987"
---
# <a name="devpkeydeviceexclusive"></a>DEVPKEY_Device_Exclusive


DEVPKEY_Device_Exclusive 设备属性表示一个布尔值，确定设备实例是否可以打开供独占使用。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_Exclusive</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>读取和写入访问权限通过安装应用程序和安装程序</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>相应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_EXCLUSIVE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_Device_Exclusive 属性的值是 DEVPROP_TRUE，如果设备可以打开以供独占使用。 否则，该属性的值为 DEVPROP_FALSE。

可以使用设置的值 DEVPKEY_Device_Exclusive [ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)包含在[ **INF *DDInstall*。硬件部分**](https://msdn.microsoft.com/library/windows/hardware/ff547330)用于安装设备。

可以检索，也可以通过调用设置的值 DEVPKEY_Device_Exclusive [ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)并[ **SetupDiSetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552163).

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_Device_Exclusive 属性键。 相反，相应的 SPDRP_EXCLUSIVE 标识符可用于访问这些早期版本的 Windows 上的属性的值。 有关如何访问这些早期版本的 Windows 上此属性的值的信息，请参阅[访问设备实例 SPDRP_Xxx 属性](https://msdn.microsoft.com/library/windows/hardware/ff537737)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)

[**INF *DDInstall*。硬件部分**](https://msdn.microsoft.com/library/windows/hardware/ff547330)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

[**SetupDiSetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552163)

 

 







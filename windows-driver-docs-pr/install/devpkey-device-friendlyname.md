---
title: DEVPKEY_Device_FriendlyName
description: DEVPKEY_Device_FriendlyName
ms.assetid: 0acea25e-5068-441b-be6b-fa863d1bdba2
keywords:
- DEVPKEY_Device_FriendlyName 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_FriendlyName
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f01dcf1ca6d06f1fa5de5642986641f91543b183
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545438"
---
# <a name="devpkeydevicefriendlyname"></a>DEVPKEY_Device_FriendlyName


DEVPKEY_Device_FriendlyName 设备属性表示设备实例的友好名称。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_FriendlyName</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>读取和写入访问权限通过安装应用程序和安装程序</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>相应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_FRIENDLYNAME</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

可以使用[ **DEVPKEY_NAME** ](devpkey-name--device-instance-.md)设备属性，而不是 DEVPKEY_Device_FriendlyName 显示标识中的用户界面显示的设备实例的名称。

可以使用设置的值 DEVPKEY_Device_FriendlyName [ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)包含在[ **INF *DDInstall*.硬件部分**](https://msdn.microsoft.com/library/windows/hardware/ff547330)安装设备的 INF 文件中。

可以通过调用检索的值 DEVPKEY_Device_FriendlyName [ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)也可以设置此属性通过调用[ **SetupDiSetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552163)。

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_Device_FriendlyName 属性键。 相反，相应的 SPDRP_FRIENDLYNAME 标识符可用于访问这些早期版本的 Windows 上的属性的值。 有关如何访问这些早期版本的 Windows 上此属性的值的信息，请参阅[访问设备实例 SPDRP_Xxx 属性](https://msdn.microsoft.com/library/windows/hardware/ff537737)。

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


[**DEVPKEY_NAME （设备实例）**](devpkey-name--device-instance-.md)

[**INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)

[**INF *DDInstall*。硬件部分**](https://msdn.microsoft.com/library/windows/hardware/ff547330)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

[**SetupDiSetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552163)

 

 







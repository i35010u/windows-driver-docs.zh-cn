---
title: DEVPKEY_Device_DriverInfSectionExt
description: DEVPKEY_Device_DriverInfSectionExt
ms.assetid: bf6260b4-5df3-4f85-8319-0f864c017e3d
keywords:
- DEVPKEY_Device_DriverInfSectionExt 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DriverInfSectionExt
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 13d93e91e048e29f26cd0568805234906ce284e0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555800"
---
# <a name="devpkeydevicedriverinfsectionext"></a>DEVPKEY_Device_DriverInfSectionExt


DEVPKEY_Device_DriverInfSectionExt 设备驱动程序属性表示的平台扩展[ **INF DDInstall 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)用于安装的设备实例的驱动程序。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_DriverInfSectionExt</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应的注册表值标识符和注册表值名称</strong></p></td>
<td align="left"><p>REGSTR_VAL_INFSECTIONEXT</p>
<p><strong>InfSectionExt</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Windows 设置 DEVPKEY_Device_DriverInfSectionExt 的值。

您可以调用[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)检索 DEVPKEY_Device_DriverInfSectionExt 值。

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_Device_DriverInfSectionExt 属性键。 在这些早期版本的 Windows 中，您可以访问此属性的值，通过访问对应**InfSectionExt**设备实例软件项下的注册表值。 有关如何访问这些早期版本的 Windows 上此属性的值的信息，请参阅[访问设备驱动程序属性](https://msdn.microsoft.com/library/windows/hardware/ff537732)。

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


[**INF DDInstall 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 







---
title: DEVPKEY_Device_UINumber
description: DEVPKEY_Device_UINumber
ms.assetid: 81bd0b71-909d-49c3-8d6c-258c57f80644
keywords:
- DEVPKEY_Device_UINumber 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_UINumber
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 01fe8ed5d9eb4262c4969cafcb9de50d2e7cf423
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386286"
---
# <a name="devpkeydeviceuinumber"></a>DEVPKEY_Device_UINumber


DEVPKEY_Device_UINumber 设备属性表示为设备实例可以在用户界面项中显示的数字。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_UINumber</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_INT32&lt;/strong&gt;](devprop-type-int32.md)"><strong>DEVPROP_TYPE_INT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>相应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_UI_NUMBER</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Windows 为 UINumber 成员的值设置的值 DEVPKEY_Device_UINumber [ **DEVICE_CAPABILITIES** ](https://msdn.microsoft.com/library/windows/hardware/ff543095)设备实例结构。 设备实例总线驱动程序返回此值以响应[ **IRP_MN_QUERY_CAPABILITIES** ](https://msdn.microsoft.com/library/windows/hardware/ff551664)请求。

您可以调用[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)检索 DEVPKEY_Device_UINumber 值。

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_Device_UINumber 属性键。 相反，相应的 SPDRP_UI_NUMBER 标识符可用于访问这些早期版本的 Windows 上的属性的值。 有关如何访问这些早期版本的 Windows 上此属性的值的信息，请参阅[访问设备实例 SPDRP_Xxx 属性](https://msdn.microsoft.com/library/windows/hardware/ff537737)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DEVICE_CAPABILITIES**](https://msdn.microsoft.com/library/windows/hardware/ff543095)

[**IRP_MN_QUERY_CAPABILITIES**](https://msdn.microsoft.com/library/windows/hardware/ff551664)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 







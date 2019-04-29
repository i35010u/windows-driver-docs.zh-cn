---
title: DEVPKEY_DeviceInterface_Enabled
description: DEVPKEY_DeviceInterface_Enabled
ms.assetid: 8e7ea36c-827d-43bd-b424-41c06ba8c20d
keywords:
- DEVPKEY_DeviceInterface_Enabled 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceInterface_Enabled
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3eacebe15dc515d84cf0364d1f0783e1991ac15c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381489"
---
# <a name="devpkeydeviceinterfaceenabled"></a>DEVPKEY_DeviceInterface_Enabled


**DeviceInterfaceEnabled**设备属性表示的布尔标志，指示是否启用设备接口。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceInterface_Enabled</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序以只读的</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果 DEVPKEY_DeviceInterface_Enabled 的值为 DEVPROP_TRUE，则启用该接口。 否则，未启用接口。

您可以调用[ **SetupDiGetDeviceInterfaceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551122)检索 DEVPKEY_DeviceInterface_Enabled 值。

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_DeviceInterface_Enabled 属性键。 有关如何检索这些早期版本的 Windows 上的设备接口的活动状态的信息，请参阅有关如何使用信息[ **SetupDiEnumDeviceInterfaces** ](https://msdn.microsoft.com/library/windows/hardware/ff551015) ，它是中提供[访问设备接口属性](https://msdn.microsoft.com/library/windows/hardware/ff537740)。

有关设备接口的详细信息，请参阅[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)并[ **INF AddInterface 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546310)。

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


[**INF AddInterface Directive**](https://msdn.microsoft.com/library/windows/hardware/ff546310)

[**SetupDiEnumDeviceInterfaces**](https://msdn.microsoft.com/library/windows/hardware/ff551015)

[**SetupDiGetDeviceInterfaceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551122)

 

 







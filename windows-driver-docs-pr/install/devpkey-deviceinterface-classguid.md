---
title: DEVPKEY_DeviceInterface_ClassGuid
description: DEVPKEY_DeviceInterface_ClassGuid
ms.assetid: f7346189-9986-4b26-b059-b1a58c8313d1
keywords:
- DEVPKEY_DeviceInterface_ClassGuid 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceInterface_ClassGuid
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3156d69db3a3ced33ad42cc32bf5c5432098ee26
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381494"
---
# <a name="devpkeydeviceinterfaceclassguid"></a>DEVPKEY_DeviceInterface_ClassGuid


DEVPKEY_DeviceInterface_ClassGuid 设备属性表示标识设备接口类的 GUID。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceInterface_ClassGuid</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-guid.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_GUID&lt;/strong&gt;](devprop-type-guid.md)"><strong>DEVPROP_TYPE_GUID</strong></a></p></td>
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

格式 {*设备接口类*} 密钥值为"{*nnnnnnnn*-*nnnn*-*nnnn* -*nnnn*-*nnnnnnnnnnnn*}"，其中每个*n*是十六进制数字。

您可以调用[ **SetupDiGetDeviceInterfaceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551122)检索 DEVPKEY_DeviceInterface_ClassGuid 值。

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_DeviceInterface_ClassGuid 属性键。 有关如何检索这些早期版本的 Windows 上的设备接口的类 GUID 的信息，请参阅有关如何使用信息[ **SetupDiEnumDeviceInterfaces** ](https://msdn.microsoft.com/library/windows/hardware/ff551015)中提供的[访问设备接口属性](https://msdn.microsoft.com/library/windows/hardware/ff537740)。

有关如何安装和访问设备接口，请参阅[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)并[ **INF AddInterface 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546310)。

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

 

 







---
title: DEVPKEY_DeviceInterface_FriendlyName
description: DEVPKEY_DeviceInterface_FriendlyName
ms.assetid: 398618a2-621b-477f-b90b-127e8df24b3d
keywords:
- DEVPKEY_DeviceInterface_FriendlyName 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceInterface_FriendlyName
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3663da355ec776d50c0519c0bd960c133f8765d8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381487"
---
# <a name="devpkeydeviceinterfacefriendlyname"></a>DEVPKEY_DeviceInterface_FriendlyName


DEVPKEY_DeviceInterface_FriendlyName 设备属性表示设备接口的友好名称。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceInterface_FriendlyName</p></td>
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
<td align="left"><p><strong>相应的注册表值名称</strong></p></td>
<td align="left"><p><strong>FriendlyName</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>是</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**FriendlyName**设置注册表值以查找设备接口类[ **INF AddInterface 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546310)包含在[ **INF *DDInstall*。接口部分**](https://msdn.microsoft.com/library/windows/hardware/ff547335)的安装设备接口的 INF 文件。

Windows 设置的值[ **DEVPKEY_NAME** ](devpkey-name--device-interface-.md) DEVPKEY_DeviceInterface_FriendlyName 的值的接口的设备属性。 若要标识用户界面项中的设备界面，用于设备接口而不是值 DEVPKEY_DeviceInterface_FriendlyName DEVPKEY_NAME 的值。

可以通过调用检索的值 DEVPKEY_DeviceInterface_FriendlyName [ **SetupDiGetDeviceInterfaceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551122)并将其设置通过调用[ **SetupDiSetDeviceInterfaceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552158)。

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_DeviceInterface_FriendlyName 属性键。 可以通过访问对应访问此属性的值**FriendlyName**设备接口的注册表条目值。 有关如何访问设备接口的注册表条目值的信息，请参阅[访问设备接口属性](https://msdn.microsoft.com/library/windows/hardware/ff537740)。

有关设备接口的信息，请参阅[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)并[ **INF AddInterface 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546310)。

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


[**DEVPKEY_NAME （设备接口）**](devpkey-name--device-interface-.md)

[**INF AddInterface Directive**](https://msdn.microsoft.com/library/windows/hardware/ff546310)

[**INF *DDInstall*。接口部分**](https://msdn.microsoft.com/library/windows/hardware/ff547335)

[**SetupDiGetDeviceInterfaceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551122)

[**SetupDiOpenDeviceInterfaceRegKey**](https://msdn.microsoft.com/library/windows/hardware/ff552075)

[**SetupDiSetDeviceInterfaceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552158)

 

 







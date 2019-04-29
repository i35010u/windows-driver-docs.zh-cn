---
title: DEVPKEY_Device_DriverRank
description: DEVPKEY_Device_DriverRank
ms.assetid: 9a6a8e9f-fd3c-4a64-b0d2-565cda0dae52
keywords:
- DEVPKEY_Device_DriverRank 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DriverRank
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e1f5489727054e3d2703bf0f829deca217a73a89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354847"
---
# <a name="devpkeydevicedriverrank"></a>DEVPKEY_Device_DriverRank


DEVPKEY_Device_DriverRank 设备属性表示为设备实例安装的驱动程序的排名。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_DriverRank</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-uint32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_UINT32&lt;/strong&gt;](devprop-type-uint32.md)"><strong>DEVPROP_TYPE_UINT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Windows 设置 DEVPKEY_Device_DriverRank 的值。

您可以调用[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)检索 DEVPKEY_Device_DriverRank 值。

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_Device_DriverRank 属性键。 有关如何访问这些早期版本的 Windows 上的此属性的信息，请参阅[访问设备驱动程序属性](https://msdn.microsoft.com/library/windows/hardware/ff537732)。

有关驱动程序级别的信息，请参阅[如何 Windows Ranks Drivers](https://msdn.microsoft.com/library/windows/hardware/ff686700) 。

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


[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

[**SetupDiGetDriverInstallParams**](https://msdn.microsoft.com/library/windows/hardware/ff551978)

[**SP_DRVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff553290)

 

 







---
title: DEVPKEY_Device_FirstInstallDate
description: DEVPKEY_Device_FirstInstallDate
ms.assetid: aedc4f18-51be-4c42-a172-c1fd88cc49b3
keywords:
- DEVPKEY_Device_FirstInstallDate 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_FirstInstallDate
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2a992ae713e7c04ba205ccbcdf2a872b43ad223f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378234"
---
# <a name="devpkeydevicefirstinstalldate"></a>DEVPKEY_Device_FirstInstallDate


DEVPKEY_Device_FirstInstallDate 设备属性指定的时间戳时在系统中首次安装设备实例。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_FirstInstallDate</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-filetime.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_FILETIME&lt;/strong&gt;](devprop-type-filetime.md)"><strong>DEVPROP_TYPE_FILETIME</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Windows 设置 DEVPKEY_Device_FirstInstallDate 的具有指定首次在系统中安装的设备实例的时间戳的值。

**请注意**  与不同[ **DEVPKEY_Device_InstallDate** ](devpkey-device-installdate.md)属性，DEVPKEY_Device_FirstInstallDate 属性的值不会更改与每个后续的更新设备驱动程序。 例如，通过 Windows Update 已更新的驱动程序不会更改此属性的值

 

您可以调用[ **SetupDiGetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)检索 DEVPKEY_Device_FirstInstallDate 属性的值。

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
<td align="left"><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 







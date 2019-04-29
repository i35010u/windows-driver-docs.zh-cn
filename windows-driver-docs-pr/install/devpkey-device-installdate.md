---
title: DEVPKEY_Device_InstallDate
description: DEVPKEY_Device_InstallDate
ms.assetid: 16b26112-1081-40f0-b65b-aafa200aa2eb
keywords:
- DEVPKEY_Device_InstallDate 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_InstallDate
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bc059a9dde25505db27108f2d48d36b348f0906c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380753"
---
# <a name="devpkeydeviceinstalldate"></a>DEVPKEY_Device_InstallDate


上次系统中安装的设备实例时，DEVPKEY_Device_InstallDate 设备属性将指定的时间戳。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_InstallDate</p></td>
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

Windows 设置具有时间戳指示上次系统中安装设备实例 DEVPKEY_Device_InstallDate 的值。

此时间戳值更改为每个连续更新的设备驱动程序。 例如，此时间戳报告的日期和时间上一次通过 Windows Update 更新设备驱动程序。

您可以调用[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)检索 DEVPKEY_Device_FirstInstallDate 属性的值。

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


[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 







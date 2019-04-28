---
title: DEVPKEY_Device_LocationInfo
description: DEVPKEY_Device_LocationInfo
ms.assetid: c7eba222-20fe-4868-89e2-9dcef9965cec
keywords:
- DEVPKEY_Device_LocationInfo 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_LocationInfo
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d642fd18306f76c8613ec552c71d00edc6d310ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351086"
---
# <a name="devpkeydevicelocationinfo"></a>DEVPKEY_Device_LocationInfo


DEVPKEY_Device_LocationInfo 设备属性表示设备实例的特定于总线的物理位置。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_LocationInfo</p></td>
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
<td align="left"><p>SPDRP_LOCATION_INFORMATION</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Windows 的 DEVPKEY_Device_LocationInfo 将值设置为总线驱动程序返回的响应中的设备实例的值[ **IRP_MN_QUERY_DEVICE_TEXT** ](https://msdn.microsoft.com/library/windows/hardware/ff551674) IRP。

您可以调用[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)并**SetupDiGetDeviceProperty**用于检索和设置 DEVPKEY_Device_LocationInfo 的值。

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_Device_LocationInfo 属性键。 相反，相应的 SPDRP_LOCATION_INFORMATION 标识符可用于访问这些早期版本的 Windows 上的属性的值。 有关如何访问这些早期版本的 Windows 上此属性的值的信息，请参阅[访问设备实例 SPDRP_Xxx 属性](https://msdn.microsoft.com/library/windows/hardware/ff537737)。

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


[**IRP_MN_QUERY_DEVICE_TEXT**](https://msdn.microsoft.com/library/windows/hardware/ff551674)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 







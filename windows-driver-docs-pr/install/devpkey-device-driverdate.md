---
title: DEVPKEY_Device_DriverDate
description: DEVPKEY_Device_DriverDate
ms.assetid: d1310b0f-f358-4875-a01b-8bc4cf8b8d2d
keywords:
- DEVPKEY_Device_DriverDate 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DriverDate
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2197597beaf004460f03a476478ba4c57d5fabc9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330573"
---
# <a name="devpkeydevicedriverdate"></a>DEVPKEY_Device_DriverDate


PKEY_Device_DriverDate 设备属性表示当前安装的驱动程序的设备实例的日期。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_DriverDate</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-filetime.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_FILETIME&lt;/strong&gt;](devprop-type-filetime.md)"><strong>DEVPROP_TYPE_FILETIME</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应的注册表值标识符和注册表值名称</strong></p></td>
<td align="left"><p>REGSTR_VAL_DRIVERDATEDATA</p>
<p><strong>DriverDateData</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_Device_DriverDate 的值由提供[ **INF DriverVer 指令**](https://msdn.microsoft.com/library/windows/hardware/ff547394)包含在**INF 版本部分**的 INF 文件的安装设备或通过特定于设备 INF **DriverVer**中包含的指令[ **INF *DDInstall*部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344) ，安装设备。

您可以调用[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)检索 DEVPKEY_Device_DriverDate 属性的值。

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_Device_DriverDate 属性键。 在这些早期版本的 Windows 中，您可以访问此属性的值，通过访问对应**DriverDateData**设备实例软件项下的注册表值。 有关如何访问这些早期版本的 Windows 上此属性的值的信息，请参阅[访问设备驱动程序属性](https://msdn.microsoft.com/library/windows/hardware/ff537732)。

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


[**INF *DDInstall*部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)

[**INF DriverVer Directive**](https://msdn.microsoft.com/library/windows/hardware/ff547394)

**INF 版本部分**
[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 







---
title: DEVPKEY_Device_GenericDriverInstalled
description: DEVPKEY_Device_GenericDriverInstalled
ms.assetid: 7809bed7-af11-42b0-bcc8-9492c47d92ab
keywords:
- DEVPKEY_Device_GenericDriverInstalled 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_GenericDriverInstalled
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 38e5e395340926b3902670efe6dc8f035f955a30
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380755"
---
# <a name="devpkeydevicegenericdriverinstalled"></a>DEVPKEY_Device_GenericDriverInstalled


DEVPKEY_Device_GenericDriverInstalled 设备属性表示一个布尔值，该值指示是否为设备实例安装的驱动程序只提供基本的设备的功能。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_GenericDriverInstalled</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
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

Windows 设置 DEVPKEY_Device_GenericDriverInstalled 的值。

DEVPKEY_Device_GenericDriverInstalled 的值设置为 DEVPROP_TRUE，指明已安装的基本驱动程序。 否则，该属性的值设置为 DEVPROP_FALSE。

您可以调用[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)检索 DEVPKEY_Device_GenericDriverInstalled 值。

Windows Server 2003、 Windows XP 和 Windows 2000 不支持此属性。

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

 

 







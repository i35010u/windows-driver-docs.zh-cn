---
title: DEVPKEY_Device_NoConnectSound
description: DEVPKEY_Device_NoConnectSound
ms.assetid: 7ed4eb3f-6585-4ec1-83b7-bde368faca0a
keywords:
- DEVPKEY_Device_NoConnectSound 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_NoConnectSound
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f9a4f097aba69bc5fcf0361135e4cb7afa00ba59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344307"
---
# <a name="devpkeydevicenoconnectsound"></a>DEVPKEY_Device_NoConnectSound


DEVPKEY_Device_NoConnectSound 设备属性表示一个布尔值，该值指示是否禁止显示 Microsoft Windows 操作系统以指示可移动设备到达或已删除的播放的声音。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_NoConnectSound</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>读取和写入访问权限通过安装应用程序和安装程序</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_Device_NoConnectSound 的值设置为 DEVPROP_TRUE 取消播放声音。 否则，该属性的值设置为 DEVPROP_FALSE。

DEVPKEY_Device_NoConnectSound 属性通常由设置[ **INF AddProperty 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546318)设备 INF 文件中。

您可以调用[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)或[ **SetupDiSetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552163)要检索或设置 DEVPKEY_Device_ 的值NoConnectSound。

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


[**INF AddProperty Directive**](https://msdn.microsoft.com/library/windows/hardware/ff546318)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 







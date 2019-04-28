---
title: DEVPKEY_DeviceClass_ClassName
description: DEVPKEY_DeviceClass_ClassName
ms.assetid: dc085e27-06c7-49ca-808f-3d1952cb8aa9
keywords:
- DEVPKEY_DeviceClass_ClassName 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_ClassName
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e04770b53f2ecd8897963a2ab18faae4692632af
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339655"
---
# <a name="devpkeydeviceclassclassname"></a>DEVPKEY_DeviceClass_ClassName


DEVPKEY_DeviceClass_ClassName 设备属性表示的类名[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_ClassName</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
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

DEVPKEY_DeviceClass_ClassName 的值将由**类**中包含的指令[ **INF 版本部分**](https://msdn.microsoft.com/library/windows/hardware/ff547394)用于安装的设备安装程序类。

您可以调用[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)或[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090)检索 DEVPKEY_DeviceClass_ 值类名。

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_DeviceClass_ClassName 属性键。 有关如何访问 Windows Server 2003、 Windows XP 和 Windows 2000 上的设备安装程序类的名称的信息，请参阅[访问的友好名称和设备安装程序类的类名称](https://msdn.microsoft.com/library/windows/hardware/ff537755)。

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


[**INF Version 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547394)

[**SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)

[**SetupDiGetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff551090)

[**SetupDiClassNameFromGuid**](https://msdn.microsoft.com/library/windows/hardware/ff550947)

 

 







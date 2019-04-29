---
title: DEVPKEY_DeviceClass_Icon
description: DEVPKEY_DeviceClass_Icon
ms.assetid: 036b6daf-b5de-4aa0-b7e3-ba0430107938
keywords:
- DEVPKEY_DeviceClass_Icon 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_Icon
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0741b53188af612d7ec36ddce55c6167f64b42e2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392532"
---
# <a name="devpkeydeviceclassicon"></a>DEVPKEY_DeviceClass_Icon


DEVPKEY_DeviceClass_Icon 设备属性表示的图标[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_Icon</p></td>
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

DEVPKEY_DeviceClass_Icon 的值将由[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)包含在[ **INF ClassInstall32 部分**](https://msdn.microsoft.com/library/windows/hardware/ff546335)用于安装类。 若要设置 DEVPKEY_DeviceClass_Icon 值，请使用**AddReg**指令设置**图标**类的注册表项值。

**图标**条目值是字符串格式的整数。 如果该数目是图标的负数，数字的绝对值是图标的 setupapi.dll 中的资源标识符。 如果数字为正，数量将是图标的类安装程序 DLL 中的资源标识符，如果没有类的安装程序或类的属性页提供程序，如果没有类安装程序，并且没有属性页提供程序。 值为零不是有效的。

您可以调用[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)或[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090)检索 DEVPKEY_DeviceClass_Icon 值.

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_DeviceClass_Icon 属性键。 有关如何访问 Windows Server 2003、 Windows XP 和 Windows 2000 上的设备安装程序类的小图标的信息，请参阅[的设备安装程序类中访问图标属性](https://msdn.microsoft.com/library/windows/hardware/ff537746)。

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


[**INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)

[**INF ClassInstall32 部分**](https://msdn.microsoft.com/library/windows/hardware/ff546335)

[**SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)

[**SetupDiGetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff551090)

[**SetupDiDrawMiniIcon**](https://msdn.microsoft.com/library/windows/hardware/ff551005)

[**SetupDiLoadClassIcon**](https://msdn.microsoft.com/library/windows/hardware/ff552053)

 

 







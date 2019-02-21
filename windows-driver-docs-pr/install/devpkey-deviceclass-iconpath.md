---
title: DEVPKEY_DeviceClass_IconPath
description: DEVPKEY_DeviceClass_IconPath
ms.assetid: c81ea18d-dd21-4b5e-8aba-52f7ad6931bf
keywords:
- DEVPKEY_DeviceClass_IconPath 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_IconPath
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c9585273aee84f3c1a01b6aff9ddf3246acfd62d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533034"
---
# <a name="devpkeydeviceclassiconpath"></a>DEVPKEY_DeviceClass_IconPath


DEVPKEY_DeviceClass_IconPath 设备属性表示的图标列表[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_IconPath</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>相应的注册表值名称</strong></p></td>
<td align="left"><p><strong>IconPath</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

您可以调用[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)或[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090)检索 DEVPKEY_DeviceClass_ 值IconPath。

DEVPKEY_DeviceClass_IconPath 当值[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-使用 Windows shell 的格式中的图标资源说明符的类型的列表。 图标资源说明符的格式是"*可执行文件的文件路径*，*资源标识符*，"位置*可执行文件的文件路径*包含完全限定的路径包含图标资源的计算机上的文件和*资源标识符*指定一个整数来标识的资源。 例如，图标资源说明符"%systemroot%\\system32\\DLL1.dll，-12"包含的可执行文件路径"%systemroot%\\system32\\DLL1.dll"和"-12"的资源标识符。

Windows Server 2003、 Windows XP 和 Windows 2000 不支持此属性。 有关如何访问这些版本的 Windows 设备安装程序类图标信息的信息，请参阅[的设备安装程序类中访问图标属性](https://msdn.microsoft.com/library/windows/hardware/ff537746)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)

[**SetupDiGetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff551090)

[**SetupDiLoadClassIcon**](https://msdn.microsoft.com/library/windows/hardware/ff552053)

 

 







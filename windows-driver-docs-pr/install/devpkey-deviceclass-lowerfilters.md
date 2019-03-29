---
title: DEVPKEY_DeviceClass_LowerFilters
description: DEVPKEY_DeviceClass_LowerFilters
ms.assetid: 39bc784e-a8be-4921-9a12-f423fe502019
keywords:
- DEVPKEY_DeviceClass_LowerFilters 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_LowerFilters
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5415eaf1f48d5788f8cdda76793dc51b5d7e2a0a
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464017"
---
# <a name="devpkeydeviceclasslowerfilters"></a>DEVPKEY_DeviceClass_LowerFilters


DEVPKEY_DeviceClass_LowerFilters 设备属性表示为安装了较低级别筛选器驱动程序的服务名称的列表[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_LowerFilters</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>数据格式</strong></p></td>
<td align="left"><p>"<em>service-name1</em>\0<em>service-name2</em>\0…<em>service-nameN</em>\0\0"</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序安装类筛选器后的只读访问权限</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>相应 SPCRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPCRP_LOWERFILTERS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>相应的注册表值名称</strong></p></td>
<td align="left"><p><strong>LowerFilters</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

类筛选器驱动程序安装时设置 DEVPKEY_DeviceClass_LowerFilters 的值。 有关如何安装类筛选器驱动程序的详细信息，请参阅[安装筛选器驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff547595)并[ **INF ClassInstall32 部分**](https://msdn.microsoft.com/library/windows/hardware/ff546335)。

您可以调用[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)或[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090)检索 DEVPKEY_DeviceClass_ 值下边的筛选程序。

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_DeviceClass_LowerFilters 属性键。 在这些早期版本的 Windows 中，您可以访问此属性的值，通过访问对应**下边的筛选程序**类注册表项下的注册表值。 有关如何访问这些早期版本的 Windows 上此属性的值的信息，请参阅[访问注册表项值下类注册表项](https://msdn.microsoft.com/library/windows/hardware/ff537751)。

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
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**INF ClassInstall32 部分**](https://msdn.microsoft.com/library/windows/hardware/ff546335)

[**SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)

[**SetupDiGetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff551090)

[**SetupDiOpenClassRegKeyEx**](https://msdn.microsoft.com/library/windows/hardware/ff552067)

 

 







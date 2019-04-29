---
title: DEVPKEY_Device_UpperFilters
description: DEVPKEY_Device_UpperFilters
ms.assetid: 5e6cba65-13ca-44b2-bb5f-ca61b3f23c5c
keywords:
- DEVPKEY_Device_UpperFilters 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_UpperFilters
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9d2ae5948a5443bb1451b09e6447b9779ba7b24b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357841"
---
# <a name="devpkeydeviceupperfilters"></a>DEVPKEY_Device_UpperFilters


DEVPKEY_Device_UpperFilters 设备属性表示为设备实例安装了较高级别筛选器驱动程序的服务名称的列表。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_UpperFilters</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>读取和写入访问权限通过安装应用程序和安装程序</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>相应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_UPPERFILTERS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

较高级别设备筛选器驱动程序安装的设备时设置 DEVPKEY_Device_UpperFilters 属性的值。 有关如何安装设备筛选器驱动程序的详细信息，请参阅[安装筛选器驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff547595)。

您可以调用[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)并**SetupDiGetDeviceProperty**用于检索和设置 DEVPKEY_Device_UpperFilters 的值。

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_Device_UpperFilters 属性键。 相反，相应的 SPDRP_UPPERFILTERS 标识符可用于访问这些早期版本的 Windows 上的属性的值。 有关如何访问这些早期版本的 Windows 上此属性的值的信息，请参阅[访问设备实例 SPDRP_Xxx 属性](https://msdn.microsoft.com/library/windows/hardware/ff537737)。

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

 

 







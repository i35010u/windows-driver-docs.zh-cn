---
title: DEVPKEY_Numa_Proximity_Domain
description: DEVPKEY_Numa_Proximity_Domain
keywords:
- DEVPKEY_Numa_Proximity_Domain 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Numa_Proximity_Domain
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 008321a6a4be919b5adcc1d854d96bc6a0066412
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801735"
---
# <a name="devpkey_numa_proximity_domain"></a>DEVPKEY_Numa_Proximity_Domain


DEVPKEY_Numa_Proximity_Domain 设备属性表示 (NUMA) 的非一致性内存体系结构的邻近域。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Numa_Proximity_Domain</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_INT32&lt;/strong&gt;](devprop-type-int32.md)"><strong>DEVPROP_TYPE_INT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问权限;设备驱动程序的读取和写入访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_Numa_Proximity_Domain 的值是表示域 ID 的数字值。

通常，操作系统通过从系统固件检索相应的信息来设置 DEVPKEY_Numa_Proximity_Domain 的值。

可以通过在设备驱动程序中调用 **IoSetDevicePropertyData** 或 **IoGetDevicePropertyData** 来检索 DEVPKEY_Numa_Proximity_Domain 的值。

你还可以调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 来检索 DEVPKEY_Numa_Proximity_Domain 的值。

此属性的值由 Windows 所有，并应由驱动程序和应用程序视为只读。

Windows Server 2003、Windows XP 和 Windows 2000 不支持此属性。

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
<td align="left"><p>可从 Windows Vista 开始使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Devpkey (包含 Devpkey) </td>
</tr>
</tbody>
</table>

 


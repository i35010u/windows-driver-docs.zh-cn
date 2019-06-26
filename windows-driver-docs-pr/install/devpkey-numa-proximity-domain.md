---
title: DEVPKEY_Numa_Proximity_Domain
description: DEVPKEY_Numa_Proximity_Domain
ms.assetid: 384e167b-cb08-4264-a7b1-3cea2dda0d46
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
ms.openlocfilehash: 9c24e1a67d6523642224bdf2854c9b03b7614996
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376805"
---
# <a name="devpkeynumaproximitydomain"></a>DEVPKEY_Numa_Proximity_Domain


DEVPKEY_Numa_Proximity_Domain 设备属性表示的邻近域的非统一内存体系结构 (NUMA)。

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
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序; 的只读访问权限读取和写入访问的设备驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_Numa_Proximity_Domain 的值是数字值，该值表示域 id。

通常情况下，操作系统通过从系统固件中检索相应信息来设置 DEVPKEY_Numa_Proximity_Domain 的值。

可以通过调用检索的值 DEVPKEY_Numa_Proximity_Domain **IoSetDevicePropertyData**或**IoGetDevicePropertyData**设备驱动程序中。

您还可以调用[ **SetupDiGetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)检索 DEVPKEY_Numa_Proximity_Domain 值。

此属性的值应由驱动程序和应用程序以只读方式处理和拥有的 Windows。

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
<td align="left"><p>提供与 Windows Vista 一起启动。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

 

 






---
title: GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR
description: GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR
ms.assetid: 163b58b1-9f88-4857-9899-32be5e9ffc3c
keywords:
- GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR
api_location:
- Ntddser.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 639f0dbbd39bd42e67d5cadd2b695912a0aa5aa7
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096917"
---
# <a name="guid_devinterface_serenum_bus_enumerator"></a>GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR


GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR [设备接口类](./overview-of-device-interface-classes.md) 定义即插即用 (PnP) [串行端口](/previous-versions/ff547451(v=vs.85))。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Attribute</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{4D36E978-E325-11CE-BFC1-08002BE10318}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供的串行端口设备枚举器注册 GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR 的实例，以通知操作系统和应用程序是否存在串行端口设备。

WDK 包含串行枚举器示例 [serenum](/previous-versions/ff546505(v=vs.85))。 Serenum 示例使用过时的标识符 [**GUID_SERENUM_BUS_ENUMERATOR**](guid-serenum-bus-enumerator.md) 来注册此设备接口类的实例。 Serenum 示例位于 WDK 的 *src \\ 内核* 目录中。

有关串行设备和驱动程序的信息，请参阅 [串行设备和驱动程序](/previous-versions/ff547451(v=vs.85))。

有关串行端口设备的设备接口类的信息，请参阅 [**GUID_DEVINTERFACE_COMPORT**](guid-devinterface-comport.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ntddser (包含 Ntddser) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**GUID_DEVINTERFACE_COMPORT**](guid-devinterface-comport.md)

[**GUID_SERENUM_BUS_ENUMERATOR**](guid-serenum-bus-enumerator.md)

 


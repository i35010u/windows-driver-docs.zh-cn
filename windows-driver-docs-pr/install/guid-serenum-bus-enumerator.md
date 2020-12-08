---
title: GUID_SERENUM_BUS_ENUMERATOR
description: GUID_SERENUM_BUS_ENUMERATOR
keywords:
- GUID_SERENUM_BUS_ENUMERATOR 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_SERENUM_BUS_ENUMERATOR
api_location:
- Ntddser.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6c58437f0189a6ee92036ac0be1157c458c89eef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808135"
---
# <a name="guid_serenum_bus_enumerator"></a>GUID_SERENUM_BUS_ENUMERATOR


GUID_SERENUM_BUS_ENUMERATOR 是 [设备接口类](./overview-of-device-interface-classes.md) 的过时标识符，适用于即插即用 (PnP) 串行端口。 从 Microsoft Windows 2000 开始，使用此类的新实例 [**GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR**](guid-devinterface-serenum-bus-enumerator.md) 类标识符。

<a name="remarks"></a>备注
-------

WDK 包括 ([*serenum*](/previous-versions/ff546505(v=vs.85))) 的串行枚举器示例。 串行枚举器使用 GUID_SERENUM_BUS_ENUMERATOR 来注册此设备接口类的实例。 Serenum 示例包含在 WDK 的 *src \\ 内核* 目录中。

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
<td align="left"><p>已过时。 从 Windows 2000 开始，改用 GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntddser (包含 Ntddser) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR**](guid-devinterface-serenum-bus-enumerator.md)

 


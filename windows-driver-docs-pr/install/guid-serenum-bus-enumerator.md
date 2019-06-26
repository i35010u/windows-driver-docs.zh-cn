---
title: GUID_SERENUM_BUS_ENUMERATOR
description: GUID_SERENUM_BUS_ENUMERATOR
ms.assetid: 85d72641-e86c-4611-9509-aea4a3344950
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
ms.openlocfilehash: 1b33951e0f97be7fd3f0e380c70b6b573d4d76e5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384782"
---
# <a name="guidserenumbusenumerator"></a>GUID_SERENUM_BUS_ENUMERATOR


GUID_SERENUM_BUS_ENUMERATOR 是已过时标识符[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)插即用 (PnP) 串行端口。 从 Microsoft Windows 2000 开始，使用[ **GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR** ](guid-devinterface-serenum-bus-enumerator.md)此类的新实例的类标识符。

<a name="remarks"></a>备注
-------

WDK 包含串行枚举器示例 ([*serenum*](https://docs.microsoft.com/previous-versions/ff546505(v=vs.85)))。 串行枚举器使用 GUID_SERENUM_BUS_ENUMERATOR 注册此设备接口类的实例。 Serenum 示例包含在*src\\内核*WDK 的目录。

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
<td align="left"><p>已过时。 从 Windows 2000 开始，请改用 GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddser.h （包括 Ntddser.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR**](guid-devinterface-serenum-bus-enumerator.md)

 

 







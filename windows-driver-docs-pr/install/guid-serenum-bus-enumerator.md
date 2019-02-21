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
ms.openlocfilehash: b5917d46e84dd6daa2b44be80eb131226c77fab4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532937"
---
# <a name="guidserenumbusenumerator"></a>GUID_SERENUM_BUS_ENUMERATOR


GUID_SERENUM_BUS_ENUMERATOR 是已过时标识符[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)插即用 (PnP) 串行端口。 从 Microsoft Windows 2000 开始，使用[ **GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR** ](guid-devinterface-serenum-bus-enumerator.md)此类的新实例的类标识符。

<a name="remarks"></a>备注
-------

WDK 包含串行枚举器示例 ([*serenum*](https://msdn.microsoft.com/library/windows/hardware/ff546505))。 串行枚举器使用 GUID_SERENUM_BUS_ENUMERATOR 注册此设备接口类的实例。 Serenum 示例包含在*src\\内核*WDK 的目录。

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
<td align="left"><p>已过时。 从 Windows 2000 开始，请改用 GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntddser.h （包括 Ntddser.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR**](guid-devinterface-serenum-bus-enumerator.md)

 

 







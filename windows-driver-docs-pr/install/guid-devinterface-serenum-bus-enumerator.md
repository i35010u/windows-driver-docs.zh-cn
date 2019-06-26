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
ms.openlocfilehash: 28fe9fdcd40a5035dee434b737f385f5237e25b3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386428"
---
# <a name="guiddevinterfaceserenumbusenumerator"></a>GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR


GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)插即用 (PnP) 定义[串行端口](https://docs.microsoft.com/previous-versions/ff547451(v=vs.85))。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">特性</th>
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

串行端口的设备的系统提供的枚举器注册 GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR 通知操作系统和应用程序的串行端口的设备存在的实例。

WDK 包含串行枚举器示例[serenum](https://docs.microsoft.com/previous-versions/ff546505(v=vs.85))。 Serenum 示例使用已过时的标识符[ **GUID_SERENUM_BUS_ENUMERATOR** ](guid-serenum-bus-enumerator.md)注册此设备接口类的实例。 Serenum 示例位于*src\\内核*WDK 的目录。

串行设备和驱动程序有关的信息，请参阅[串行设备和驱动程序](https://docs.microsoft.com/previous-versions/ff547451(v=vs.85))。

串行端口的设备的设备接口类有关的信息，请参阅[ **GUID_DEVINTERFACE_COMPORT**](guid-devinterface-comport.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntddser.h （包括 Ntddser.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_DEVINTERFACE_COMPORT**](guid-devinterface-comport.md)

[**GUID_SERENUM_BUS_ENUMERATOR**](guid-serenum-bus-enumerator.md)

 

 







---
title: GUID_DEVINTERFACE_DISPLAY_ADAPTER
description: GUID_DEVINTERFACE_DISPLAY_ADAPTER
ms.assetid: 22f705b0-bc79-43e8-8445-adf611ae1429
keywords:
- GUID_DEVINTERFACE_DISPLAY_ADAPTER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_DISPLAY_ADAPTER
api_location:
- Ntddvdeo.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 325fb4ca0c437e29f742ee6a9465ad8303fcd740
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322181"
---
# <a name="guiddevinterfacedisplayadapter"></a>GUID_DEVINTERFACE_DISPLAY_ADAPTER


GUID_DEVINTERFACE_DISPLAY_ADAPTER[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为受支持的显示视图以显示适配器定义。

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
<td align="left"><p>GUID_DEVINTERFACE_DISPLAY_ADAPTER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{5B45201D-F2F2-4F3B-85BB-30FF1F953599}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供显示器驱动程序注册此设备接口类，以通知操作系统和应用程序的显示视图状态的实例。

显示设备的信息，请参阅[Windows Vista 显示器驱动程序模型](https://msdn.microsoft.com/library/windows/hardware/ff570593)并[Windows 2000 显示器驱动程序模型](https://msdn.microsoft.com/library/windows/hardware/ff570584)。

有关显示适配器的设备接口类的信息，请参阅[ **GUID_DISPLAY_DEVICE_ARRIVAL**](guid-display-device-arrival.md)。

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
<td align="left">Ntddvdeo.h （包括 Ntddvdeo.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_DISPLAY_DEVICE_ARRIVAL**](guid-display-device-arrival.md)

 

 







---
title: GUID_DEVINTERFACE_MEDIUMCHANGER
description: GUID_DEVINTERFACE_MEDIUMCHANGER
ms.assetid: d7c41c5c-b03b-459e-81b0-b363b4c174b0
keywords:
- GUID_DEVINTERFACE_MEDIUMCHANGER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_MEDIUMCHANGER
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 14f150a1affa917061dfb303d937828a134b24b2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386434"
---
# <a name="guiddevinterfacemediumchanger"></a>GUID_DEVINTERFACE_MEDIUMCHANGER


GUID_DEVINTERFACE_MEDIUMCHANGER[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为介质转换器的设备定义。

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
<td align="left"><p>GUID_DEVINTERFACE_MEDIUMCHANGER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{53F56310-B6BF-11D0-94F2-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供中型[更换器驱动程序](https://docs.microsoft.com/windows-hardware/drivers/storage/changer-drivers)注册 GUID_DEVINTERFACE_MEDIUMCHANGER 通知操作系统和应用程序的媒体更换器设备是否存在的实例。

有关存储驱动程序的详细信息，请参阅[存储设备驱动程序](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-drivers)。

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
<td align="left">Ntddstor.h （包括 Ntddstor.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**MediumChangerClassGuid**](mediumchangerclassguid.md)

 

 







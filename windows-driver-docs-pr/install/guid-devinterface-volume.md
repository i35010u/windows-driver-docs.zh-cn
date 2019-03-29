---
title: GUID_DEVINTERFACE_VOLUME
description: GUID_DEVINTERFACE_VOLUME
ms.assetid: 34802df4-8a8f-48ea-a146-d2ad4ae4709a
keywords:
- GUID_DEVINTERFACE_VOLUME 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_VOLUME
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3e55c378c959995961562e15b127749a7b93bee5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564947"
---
# <a name="guiddevinterfacevolume"></a>GUID_DEVINTERFACE_VOLUME


GUID_DEVINTERFACE_VOLUME[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为卷设备定义。

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
<td align="left"><p>GUID_DEVINTERFACE_VOLUME</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{53F5630D-B6BF-11D0-94F2-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供[存储类驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff559215)注册 GUID_DEVINTERFACE_VOLUME 通知操作系统和应用程序的卷设备的状态的实例。 计数管理器使用插即用 (PnP) 设备接口通知机制来发出信号的到达或删除卷接口。

存储[示例](https://go.microsoft.com/fwlink/p/?LinkId=618052)WDK 中包括[Addfilter 存储筛选器工具](https://go.microsoft.com/fwlink/p/?linkid=256076)使用已过时的标识符[ **VolumeClassGuid** ](volumeclassguid.md)若要枚举 GUID_DEVINTERFACE_VOLUME 设备接口类的实例。

有关存储驱动程序的详细信息，请参阅[存储设备驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff566976)并[存储类驱动程序中支持装入管理器请求](https://msdn.microsoft.com/library/windows/hardware/ff567603)。

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


[**VolumeClassGuid**](volumeclassguid.md)

 

 







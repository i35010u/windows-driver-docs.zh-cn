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
ms.openlocfilehash: d0fbad23941f885d5229fbd39e5763c14aec27c3
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733515"
---
# <a name="guid_devinterface_volume"></a>GUID_DEVINTERFACE_VOLUME


为卷设备定义 GUID_DEVINTERFACE_VOLUME [设备接口类](./overview-of-device-interface-classes.md) 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
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

系统提供的 [存储类驱动程序](../storage/introduction-to-storage-class-drivers.md) 将注册 GUID_DEVINTERFACE_VOLUME 的实例，以通知操作系统和应用程序是否存在卷设备。 装载管理器使用即插即用 (PnP) 设备接口通知机制来通知到达或删除卷接口。

WDK 中的存储 [示例](https://go.microsoft.com/fwlink/p/?LinkId=618052) 包括一个 [Addfilter 存储筛选器工具](/samples/browse/) ，该工具使用过时的标识符 [**VolumeClassGuid**](volumeclassguid.md) 来枚举 GUID_DEVINTERFACE_VOLUME 设备接口类的实例。

有关存储驱动程序的详细信息，请参阅存储类驱动程序中的 [存储驱动程序](../storage/storage-drivers.md) 和 [支持装入管理器请求](../storage/supporting-mount-manager-requests-in-a-storage-class-driver.md)。

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
<td align="left">Ntddstor (包含 Ntddstor) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**VolumeClassGuid**](volumeclassguid.md)


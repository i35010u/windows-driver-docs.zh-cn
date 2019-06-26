---
title: VolumeClassGuid
description: VolumeClassGuid
ms.assetid: 30d0db03-fbea-4245-b8d7-ca3a06a54861
keywords:
- VolumeClassGuid 设备和驱动程序安装
topic_type:
- apiref
api_name:
- VolumeClassGuid
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c7d2684d127ace4921c38df7e238cac73619916e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380404"
---
# <a name="volumeclassguid"></a>VolumeClassGuid


VolumeClassGuid 是已过时标识符[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)卷设备。 从 Microsoft Windows 2000 开始，使用[ **GUID_DEVINTERFACE_VOLUME** ](guid-devinterface-volume.md)此类的新实例的类标识符。

<a name="remarks"></a>备注
-------

存储[示例](https://go.microsoft.com/fwlink/p/?LinkId=618052)WDK 中包括[Addfilter 存储筛选器工具](https://go.microsoft.com/fwlink/p/?linkid=256076)，它使用 VolumeClassGuid 枚举的实例[ **GUID_DEVINTERFACE_VOLUME**](guid-devinterface-volume.md)设备接口类。

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
<td align="left"><p>已过时。 从 Windows 2000 开始，请改用 GUID_DEVINTERFACE_VOLUME。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddstor.h （包括 Ntddstor.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_DEVINTERFACE_VOLUME**](guid-devinterface-volume.md)

 

 







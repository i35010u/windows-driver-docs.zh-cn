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
ms.openlocfilehash: b636807af2c4425baa7b058f7cdf4b22929187f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554607"
---
# <a name="volumeclassguid"></a>VolumeClassGuid


VolumeClassGuid 是已过时标识符[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)卷设备。 从 Microsoft Windows 2000 开始，使用[ **GUID_DEVINTERFACE_VOLUME** ](guid-devinterface-volume.md)此类的新实例的类标识符。

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
<td align="left"><p>版本</p></td>
<td align="left"><p>已过时。 从 Windows 2000 开始，请改用 GUID_DEVINTERFACE_VOLUME。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntddstor.h （包括 Ntddstor.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**GUID_DEVINTERFACE_VOLUME**](guid-devinterface-volume.md)

 

 







---
title: FloppyClassGuid
description: FloppyClassGuid
ms.assetid: 60811704-0a59-48b4-b9c6-baf6c0f8c1c2
keywords:
- FloppyClassGuid 设备和驱动程序安装
topic_type:
- apiref
api_name:
- FloppyClassGuid
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3826c82d3cc380e3d650e7b9ece1421ce1ab5ce8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360283"
---
# <a name="floppyclassguid"></a>FloppyClassGuid


FloppyClassGuid 是已过时标识符[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)的软盘[存储设备](https://docs.microsoft.com/windows-hardware/drivers/storage/index)。 从 Microsoft Windows 2000 开始，使用[ **GUID_DEVINTERFACE_FLOPPY** ](guid-devinterface-floppy.md)此类的新实例的类标识符。

<a name="remarks"></a>备注
-------

存储[示例](https://go.microsoft.com/fwlink/p/?LinkId=618052)WDK 中包括[软盘驱动程序](https://go.microsoft.com/fwlink/p/?linkid=256192)此示例使用 FloppyClassGuid 来注册此设备接口类的实例。

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
<td align="left"><p>已过时。 从 Windows 2000 开始，请改用 GUID_DEVINTERFACE_FLOPPY。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddstor.h （包括 Ntddstor.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_DEVINTERFACE_FLOPPY**](guid-devinterface-floppy.md)

 

 







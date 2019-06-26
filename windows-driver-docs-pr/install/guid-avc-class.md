---
title: GUID_AVC_CLASS
description: GUID_AVC_CLASS
ms.assetid: 1aa323d3-7d68-4c50-af68-01bda3792fec
keywords:
- GUID_AVC_CLASS 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_AVC_CLASS
api_location:
- Avc.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c4464c1d50e8bb3c4f21cb73fc93479c7d2b7888
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387328"
---
# <a name="guidavcclass"></a>GUID_AVC_CLASS


GUID_AVC_CLASS[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)定义为受支持的音频视频控件 (AV/C) 设备[AVStream](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-overview)体系结构。

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
<td align="left"><p>GUID_AVC_CLASS</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{095780C3-48A1-4570-BD95-46707F78C2DC}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供[AV/C 客户端驱动程序](https://docs.microsoft.com/windows-hardware/drivers/stream/av-c-client-drivers2) [Avc.sys](https://docs.microsoft.com/windows-hardware/drivers/stream/using-avc-sys)注册 GUID_AVC_CLASS 可以表示外部 AV/C 单元的 1394年总线上的实例。

AV/C 的虚拟设备的设备接口类有关的信息，请参阅[ **GUID_VIRTUAL_AVC_CLASS**](guid-virtual-avc-class.md)。

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
<td align="left"><p>在 Windows Vista、 Windows Server 2003、 Windows XP 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Avc.h （包括 Avc.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_VIRTUAL_AVC_CLASS**](guid-virtual-avc-class.md)

 

 







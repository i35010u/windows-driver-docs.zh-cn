---
title: GUID_VIRTUAL_AVC_CLASS
description: GUID_VIRTUAL_AVC_CLASS
ms.assetid: bd577fd7-f50c-4477-9619-8dd9e849367a
keywords:
- GUID_VIRTUAL_AVC_CLASS 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_VIRTUAL_AVC_CLASS
api_location:
- Avc.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 138f560c505ef6bdb640d39cd7dd172b72e431ba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383860"
---
# <a name="guidvirtualavcclass"></a>GUID_VIRTUAL_AVC_CLASS


GUID_VIRTUAL_AVC_CLASS[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)定义为受支持的虚拟音频视频控件 (AV/C) 设备[AVStream](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-overview)体系结构。

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
<td align="left"><p>GUID_VIRTUAL_AVC_CLASS</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{616EF4D0-23CE-446D-A568-C31EB01913D0}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供[AV/C 客户端驱动程序](https://docs.microsoft.com/windows-hardware/drivers/stream/av-c-client-drivers2) [Avc.sys](https://docs.microsoft.com/windows-hardware/drivers/stream/using-avc-sys)注册 GUID_VIRTUAL_AVC_CLASS 来表示虚拟 AV/C 设备的实例。

了解设备接口类的 AV/C 单位的 1394年总线上，请参阅[ **GUID_AVC_CLASS**](guid-avc-class.md)。

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
<td align="left"><p>在 Windows Vista、 Microsoft Windows Server 2003、 Windows XP 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Avc.h （包括 Avc.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_AVC_CLASS**](guid-avc-class.md)

 

 







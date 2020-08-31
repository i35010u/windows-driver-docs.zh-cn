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
ms.openlocfilehash: 906d232f36fe05f66e950d56ab3f0c5da95c59b2
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095713"
---
# <a name="guid_avc_class"></a>GUID_AVC_CLASS


GUID_AVC_CLASS [设备接口类](./overview-of-device-interface-classes.md) 是为音频视频控制定义的 (AV/C) 设备受 [AVStream](../stream/avstream-overview.md) 的体系结构支持。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Attribute</th>
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

系统提供的 [AV/C 客户端驱动程序](../stream/av-c-client-drivers2.md) [Avc.sys](../stream/using-avc-sys.md) 注册 GUID_AVC_CLASS 的实例，以表示1394总线上的外部 AV/c 单元。

有关虚拟 AV/C 设备的设备接口类的信息，请参阅 [**GUID_VIRTUAL_AVC_CLASS**](guid-virtual-avc-class.md)。

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
<td align="left"><p>在 Windows Vista、Windows Server 2003、Windows XP 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Avc (包含 Avc) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**GUID_VIRTUAL_AVC_CLASS**](guid-virtual-avc-class.md)

 


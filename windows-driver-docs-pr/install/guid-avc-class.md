---
title: GUID_AVC_CLASS
description: GUID_AVC_CLASS
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
ms.openlocfilehash: c2e50dc5238045e6f7b35a36515cdc3d49666e79
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822323"
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

系统提供的 [AV/C 客户端驱动程序](../stream/av-c-client-drivers2.md) [Avc.sys](../stream/using-avc-sys.md) 注册 GUID_AVC_CLASS 的实例，以表示1394总线上的外部 AV/c 单元。

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

## <a name="see-also"></a>请参阅


[**GUID_VIRTUAL_AVC_CLASS**](guid-virtual-avc-class.md)

 


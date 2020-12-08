---
title: GUID_VIRTUAL_AVC_CLASS
description: GUID_VIRTUAL_AVC_CLASS
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
ms.openlocfilehash: 481b8c81cddf5a8d474cfa2ce823aa6c8e176801
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831399"
---
# <a name="guid_virtual_avc_class"></a>GUID_VIRTUAL_AVC_CLASS


GUID_VIRTUAL_AVC_CLASS [设备接口类](./overview-of-device-interface-classes.md) 是为虚拟音频视频控制定义的 (AV/C) 设备受 [AVStream](../stream/avstream-overview.md) 的体系结构支持。

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

系统提供的 [AV/c 客户端驱动程序](../stream/av-c-client-drivers2.md) [Avc.sys](../stream/using-avc-sys.md) 注册 GUID_VIRTUAL_AVC_CLASS 的实例，以表示虚拟 AV/c 设备。

有关1394总线上 AV/C 设备的设备接口类的信息，请参阅 [**GUID_AVC_CLASS**](guid-avc-class.md)。

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
<td align="left"><p>在 Windows Vista、Microsoft Windows Server 2003、Windows XP 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Avc (包含 Avc) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_AVC_CLASS**](guid-avc-class.md)

 


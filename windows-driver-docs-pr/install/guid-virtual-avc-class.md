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
ms.openlocfilehash: 6b757be14631fcd2da5b1b78b90457e59165b57f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576212"
---
# <a name="guidvirtualavcclass"></a>GUID_VIRTUAL_AVC_CLASS


GUID_VIRTUAL_AVC_CLASS[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)定义为受支持的虚拟音频视频控件 (AV/C) 设备[AVStream](https://msdn.microsoft.com/library/windows/hardware/ff554240)体系结构。

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

系统提供[AV/C 客户端驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff556367) [Avc.sys](https://msdn.microsoft.com/library/windows/hardware/ff568667)注册 GUID_VIRTUAL_AVC_CLASS 来表示虚拟 AV/C 设备的实例。

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
<td align="left"><p>版本</p></td>
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

 

 







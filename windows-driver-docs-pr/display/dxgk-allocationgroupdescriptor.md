---
title: '\_DXGK\_ALLOCATIONGROUPDESCRIPTOR 结构'
description: DXGK\_ALLOCATIONGROUPDESCRIPTOR 结构保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: 74ca560d-b5ec-40f1-a064-4972c7908fc9
keywords:
- _DXGK_ALLOCATIONGROUPDESCRIPTOR 结构显示设备
- DXGK_ALLOCATIONGROUPDESCRIPTOR 结构显示设备
topic_type:
- apiref
api_name:
- DXGK_ALLOCATIONGROUPDESCRIPTOR
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: f5b8c7149b7664b78fd4a20e20fde5d0f4be6c16
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548082"
---
# <a name="dxgkallocationgroupdescriptor-structure"></a>\_DXGK\_ALLOCATIONGROUPDESCRIPTOR 结构


DXGK\_ALLOCATIONGROUPDESCRIPTOR 结构保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_ALLOCATIONGROUPDESCRIPTOR {
  D3DGPU_VIRTUAL_ADDRESS MinimumVirtualAddress;
  D3DGPU_VIRTUAL_ADDRESS MaximumVirtualAddress;
} DXGK_ALLOCATIONGROUPDESCRIPTOR;
```

<a name="members"></a>成员
-------

**MinimumVirtualAddress**保留供系统使用。

**MaximumVirtualAddress**保留供系统使用。

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
<td align="left"><p>在 Windows 7 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">D3dkmddi.h （包括 D3dkmddi.h）</td>
</tr>
</tbody>
</table>

 

 






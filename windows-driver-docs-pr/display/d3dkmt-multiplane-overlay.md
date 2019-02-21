---
title: D3DKMT\_MULTIPLANE\_覆盖结构
description: 保留供系统使用。 不要在您的驱动程序中使用。
ms.assetid: 54773231-6240-4f44-9aff-706616af68b6
keywords:
- D3DKMT_MULTIPLANE_OVERLAY 结构显示设备
topic_type:
- apiref
api_name:
- D3DKMT_MULTIPLANE_OVERLAY
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: bb52e7c75bae01ae4b436982bd0cb9f7826690e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520354"
---
# <a name="d3dkmtmultiplaneoverlay-structure"></a>D3DKMT\_MULTIPLANE\_覆盖结构


保留供系统使用。 不要在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct D3DKMT_MULTIPLANE_OVERLAY {
  UINT                                 LayerIndex;
  BOOL                                 Enabled;
  D3DKMT_HANDLE                        hAllocation;
  D3DKMT_MULTIPLANE_OVERLAY_ATTRIBUTES PlaneAttributes;
} D3DKMT_MULTIPLANE_OVERLAY;
```

<a name="members"></a>成员
-------

**LayerIndex**

**已启用**

**hAllocation**

**PlaneAttributes**

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>最低受支持的客户端</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">D3dkmthk.h</td>
</tr>
</tbody>
</table>

 

 






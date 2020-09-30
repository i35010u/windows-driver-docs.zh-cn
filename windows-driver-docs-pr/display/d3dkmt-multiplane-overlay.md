---
title: D3DKMT \_ MULTIPLANE \_ 覆盖结构
description: 了解 D3DKMT \_ MULTIPLANE \_ 覆盖结构，该结构已保留供系统使用。 请勿在您的驱动程序中使用。
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
ms.openlocfilehash: a746f6f313e69c997d43839caa3aaf6b2980037f
ms.sourcegitcommit: f1d6c2d0cdbecdc69ba65ed3b530755fc73c8e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91590389"
---
# <a name="d3dkmt_multiplane_overlay-structure"></a>D3DKMT \_ MULTIPLANE \_ 覆盖结构


预留给系统使用。 请勿在您的驱动程序中使用。

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
<td align="left">D3dkmthk</td>
</tr>
</tbody>
</table>

 

 






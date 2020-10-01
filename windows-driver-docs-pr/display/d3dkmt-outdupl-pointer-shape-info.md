---
title: D3DKMT \_ OUTDUPL \_ 指针 \_ 形状 \_ 信息结构
description: 了解 D3DKMT \_ OUTDUPL \_ 指针 \_ 形状 \_ 信息结构，该结构已保留供系统使用。 请勿在您的驱动程序中使用。
ms.assetid: fc72fe82-8807-44ac-b9da-8f84d38c45bf
keywords:
- D3DKMT_OUTDUPL_POINTER_SHAPE_INFO 结构显示设备
topic_type:
- apiref
api_name:
- D3DKMT_OUTDUPL_POINTER_SHAPE_INFO
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9f748b000e9e7a61fffcfa2b08e9d77655f62c84
ms.sourcegitcommit: fc94eb0d5a41ef81c1b3ab91ad725386db0be0c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603596"
---
# <a name="d3dkmt_outdupl_pointer_shape_info-structure"></a>D3DKMT \_ OUTDUPL \_ 指针 \_ 形状 \_ 信息结构


预留给系统使用。 请勿在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _D3DKMT_OUTDUPL_POINTER_SHAPE_INFO {
  D3DKMT_OUTDUPL_POINTER_SHAPE_TYPE Type;
  UINT                              Width;
  UINT                              Height;
  UINT                              Pitch;
  POINT                             HotSpot;
} D3DKMT_OUTDUPL_POINTER_SHAPE_INFO;
```

<a name="members"></a>成员
-------

**类型**

Width 

Height 

**音调**

**地区**

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
<td align="left">D3dkmthk (包含 D3dkmthk) </td>
</tr>
</tbody>
</table>

 

 






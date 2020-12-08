---
title: '\_DXGKARG \_ UPDATEPAGETABLEFLAGS 结构'
description: DXGKARG \_ UPDATEPAGETABLEFLAGS 结构保留供系统使用。 不要在您的驱动程序中使用它。
keywords:
- _DXGKARG_UPDATEPAGETABLEFLAGS 结构显示设备
- DXGKARG_UPDATEPAGETABLEFLAGS 结构显示设备
topic_type:
- apiref
api_name:
- DXGKARG_UPDATEPAGETABLEFLAGS
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 080f853c6f6beeb3c5eb35b2d258e82a6c0c31f7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808955"
---
# <a name="_dxgkarg_updatepagetableflags-structure"></a>\_DXGKARG \_ UPDATEPAGETABLEFLAGS 结构


DXGKARG \_ UPDATEPAGETABLEFLAGS 结构保留供系统使用。 不要在您的驱动程序中使用它。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGKARG_UPDATEPAGETABLEFLAGS {
  union {
    struct {
      UINT LinearAccess  :1;
      UINT Reserved  :31;
    };
    UINT Value;
  };
} DXGKARG_UPDATEPAGETABLEFLAGS;
```

<a name="members"></a>成员
-------

**LinearAccess** 保留供系统使用。

**保留** 保留供系统使用。

**值** 保留供系统使用。

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
<td align="left"><p>在 windows 7 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">D3dkmddi (包含 D3dkmddi) </td>
</tr>
</tbody>
</table>

 

 






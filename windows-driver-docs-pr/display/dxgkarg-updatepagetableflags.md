---
title: '\_DXGKARG\_UPDATEPAGETABLEFLAGS 结构'
description: DXGKARG\_UPDATEPAGETABLEFLAGS 结构保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: 59a3fb51-ba3e-420e-abf7-c3faacc25ebc
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
ms.openlocfilehash: 6370ee8b5f683871ce957c889cc3e240edf56fc3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384462"
---
# <a name="dxgkargupdatepagetableflags-structure"></a>\_DXGKARG\_UPDATEPAGETABLEFLAGS 结构


DXGKARG\_UPDATEPAGETABLEFLAGS 结构保留供系统使用。 不要使用它在您的驱动程序中。

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

**LinearAccess**保留供系统使用。

**保留**保留供系统使用。

**值**保留供系统使用。

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
<td align="left"><p>在 Windows 7 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">D3dkmddi.h （包括 D3dkmddi.h）</td>
</tr>
</tbody>
</table>

 

 






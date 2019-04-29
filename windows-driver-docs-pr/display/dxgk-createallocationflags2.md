---
title: '\_DXGK\_CREATEALLOCATIONFLAGS2 结构'
description: DXGK\_CREATEALLOCATIONFLAGS2 结构保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: c0d57a64-c509-4d72-81eb-7591bb0c1b9b
keywords:
- _DXGK_CREATEALLOCATIONFLAGS2 结构显示设备
- DXGK_CREATEALLOCATIONFLAGS2 结构显示设备
topic_type:
- apiref
api_name:
- DXGK_CREATEALLOCATIONFLAGS2
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: be2ec4413767a24b09ee9e7b880731a956e5b5d4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389987"
---
# <a name="dxgkcreateallocationflags2-structure"></a>\_DXGK\_CREATEALLOCATIONFLAGS2 结构


DXGK\_CREATEALLOCATIONFLAGS2 结构保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_CREATEALLOCATIONFLAGS2 {
  union {
    struct {
      UINT Resource;
      UINT Reserved;
    };
    UINT Value;
  };
} DXGK_CREATEALLOCATIONFLAGS2;
```

<a name="members"></a>成员
-------

**资源**保留供系统使用。

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

 

 






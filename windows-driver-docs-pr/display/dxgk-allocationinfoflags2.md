---
title: '\_DXGK\_ALLOCATIONINFOFLAGS2 结构'
description: DXGK\_ALLOCATIONINFOFLAGS2 结构保留供系统使用。 不要在您的驱动程序中使用。
ms.assetid: 67c27f53-29f0-4639-a360-0dbf7f3b3849
keywords:
- _DXGK_ALLOCATIONINFOFLAGS2 结构显示设备
- DXGK_ALLOCATIONINFOFLAGS2 结构显示设备
topic_type:
- apiref
api_name:
- DXGK_ALLOCATIONINFOFLAGS2
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: e868b54ec7dec952c338f98cdcc02b35e69c258f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554464"
---
# <a name="dxgkallocationinfoflags2-structure"></a>\_DXGK\_ALLOCATIONINFOFLAGS2 结构


DXGK\_ALLOCATIONINFOFLAGS2 结构保留供系统使用。 不要在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_ALLOCATIONINFOFLAGS2 {
  union {
    struct {
      UINT CpuVisible;
      UINT ReadOnly;
      UINT PermanentSysMem;
      UINT Cached;
      UINT ExistingSysMem;
      UINT ExistingKernelSysMem;
      UINT Swizzled;
      UINT Overlay;
      UINT Capture;
      UINT SynchronousPaging;
      UINT LinkMirrored;
      UINT LinkInstanced;
      UINT HistoryBuffer  :1;
      UINT Reserved  :2;
      UINT DXGK_ALLOC_RESERVED16  :1;
      UINT DXGK_ALLOC_RESERVED15  :1;
      UINT DXGK_ALLOC_RESERVED14  :1;
      UINT DXGK_ALLOC_RESERVED13  :1;
      UINT DXGK_ALLOC_RESERVED12  :1;
      UINT DXGK_ALLOC_RESERVED11  :1;
      UINT DXGK_ALLOC_RESERVED9  :1;
      UINT DXGK_ALLOC_RESERVED8  :1;
      UINT DXGK_ALLOC_RESERVED7  :1;
      UINT DXGK_ALLOC_RESERVED6  :1;
      UINT DXGK_ALLOC_RESERVED5  :1;
      UINT DXGK_ALLOC_RESERVED4  :1;
      UINT DXGK_ALLOC_RESERVED3  :1;
      UINT DXGK_ALLOC_RESERVED2  :1;
      UINT DXGK_ALLOC_RESERVED1  :1;
      UINT DXGK_ALLOC_RESERVED0  :1;
    };
    UINT Value;
  };
} DXGK_ALLOCATIONINFOFLAGS2;
```

<a name="members"></a>成员
-------

**CpuVisible**

**ReadOnly**

**PermanentSysMem**

**缓存**

**ExistingSysMem**

**ExistingKernelSysMem**

**Swizzled**

**Overlay**

**Capture**

**SynchronousPaging**

**LinkMirrored**

**LinkInstanced**

**HistoryBuffer**

**保留**

**DXGK\_ALLOC\_RESERVED16**

**DXGK\_ALLOC\_RESERVED15**

**DXGK\_ALLOC\_RESERVED14**

**DXGK\_ALLOC\_RESERVED13**

**DXGK\_ALLOC\_RESERVED12**

**DXGK\_ALLOC\_RESERVED11**

**DXGK\_ALLOC\_RESERVED9**

**DXGK\_ALLOC\_RESERVED8**

**DXGK\_ALLOC\_RESERVED7**

**DXGK\_ALLOC\_RESERVED6**

**DXGK\_ALLOC\_RESERVED5**

**DXGK\_ALLOC\_RESERVED4**

**DXGK\_ALLOC\_RESERVED3**

**DXGK\_ALLOC\_RESERVED2**

**DXGK\_ALLOC\_RESERVED1**

**DXGK\_ALLOC\_RESERVED0**

**值**

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
<td align="left"><p>在 Windows 7 和更高版本的 Windows 操作系统中可用。 在 Windows 8.1 中更新。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">D3dkmddi.h （包括 D3dkmddi.h）</td>
</tr>
</tbody>
</table>

 

 






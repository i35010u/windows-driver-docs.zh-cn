---
title: '\_DXGK \_ ALLOCATIONINFOFLAGS2 结构'
description: DXGK \_ ALLOCATIONINFOFLAGS2 结构保留供系统使用。 请勿在您的驱动程序中使用。
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
ms.openlocfilehash: 7a63d58eeaf1c242bfa9e81e6ed238cf3fbd5afa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809059"
---
# <a name="_dxgk_allocationinfoflags2-structure"></a>\_DXGK \_ ALLOCATIONINFOFLAGS2 结构


DXGK \_ ALLOCATIONINFOFLAGS2 结构保留供系统使用。 请勿在您的驱动程序中使用。

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

**Cached（缓存的请求）**

**ExistingSysMem**

**ExistingKernelSysMem**

**Swizzled**

**叠加**

**捕获**

**SynchronousPaging**

**LinkMirrored**

**LinkInstanced**

**HistoryBuffer**

Reserved 

**DXGK \_ 分配 \_ RESERVED16**

**DXGK \_ 分配 \_ RESERVED15**

**DXGK \_ 分配 \_ RESERVED14**

**DXGK \_ 分配 \_ RESERVED13**

**DXGK \_ 分配 \_ RESERVED12**

**DXGK \_ 分配 \_ RESERVED11**

**DXGK \_ 分配 \_ RESERVED9**

**DXGK \_ 分配 \_ RESERVED8**

**DXGK \_ 分配 \_ RESERVED7**

**DXGK \_ 分配 \_ RESERVED6**

**DXGK \_ 分配 \_ RESERVED5**

**DXGK \_ 分配 \_ RESERVED4**

**DXGK \_ 分配 \_ RESERVED3**

**DXGK \_ 分配 \_ RESERVED2**

**DXGK \_ 分配 \_ RESERVED1**

**DXGK \_ 分配 \_ RESERVED0**

值

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
<td align="left"><p>在 windows 7 和更高版本的 Windows 操作系统中可用。 已在 Windows 8.1 中更新。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">D3dkmddi (包含 D3dkmddi) </td>
</tr>
</tbody>
</table>

 

 






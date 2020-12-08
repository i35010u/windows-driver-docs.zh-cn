---
title: D3DKMT \_ 存在 \_ MULTIPLANE \_ 覆盖结构
description: 了解 D3DKMT 存在的 \_ \_ MULTIPLANE \_ 覆盖结构，该结构已保留供系统使用。 请勿在您的驱动程序中使用。
keywords:
- D3DKMT_PRESENT_MULTIPLANE_OVERLAY 结构显示设备
topic_type:
- apiref
api_name:
- D3DKMT_PRESENT_MULTIPLANE_OVERLAY
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1643298f6c6499137362614ccb5bfcb9d83ea658
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819607"
---
# <a name="d3dkmt_present_multiplane_overlay-structure"></a>D3DKMT \_ 存在 \_ MULTIPLANE \_ 覆盖结构


预留给系统使用。 请勿在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct D3DKMT_PRESENT_MULTIPLANE_OVERLAY {
  union {
    D3DKMT_HANDLE hDevice;
    D3DKMT_HANDLE hContext;
  };
  ULONG                          BroadcastContextCount;
  D3DKMT_HANDLE                  BroadcastContext[D3DDDI_MAX_BROADCAST_CONTEXT];
  D3DDDI_VIDEO_PRESENT_SOURCE_ID VidPnSourceId;
  UINT                           PresentCount;
  D3DDDI_FLIPINTERVAL_TYPE       FlipInterval;
  D3DKMT_PRESENTFLAGS            Flags;
  UINT                           PresentPlaneCount;
  D3DKMT_MULTIPLANE_OVERLAY      *pPresentPlanes;
  UINT                           Duration;
} D3DKMT_PRESENT_MULTIPLANE_OVERLAY;
```

<a name="members"></a>成员
-------

**hDevice**

**hContext**

**BroadcastContextCount**

**BroadcastContext**

**VidPnSourceId**

**PresentCount**

**FlipInterval**

**标记**

**PresentPlaneCount**

**pPresentPlanes**

**Duration**

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

 

 






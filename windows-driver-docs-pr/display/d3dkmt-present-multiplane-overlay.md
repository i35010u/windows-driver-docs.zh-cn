---
title: D3DKMT\_存在\_MULTIPLANE\_覆盖结构
description: 保留供系统使用。 不要在您的驱动程序中使用。
ms.assetid: 2526ccce-826a-4e8f-ab15-639510b1d5cf
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
ms.openlocfilehash: bc406f672581819e08752986980c086187797e89
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519955"
---
# <a name="d3dkmtpresentmultiplaneoverlay-structure"></a>D3DKMT\_存在\_MULTIPLANE\_覆盖结构


保留供系统使用。 不要在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct D3DKMT_PRESENT_MULTIPLANE_OVERLAY {
  union {
    D3DKMT_HANDLE hDevice;
    D3DKMT_HANDLE hContext;
  };
  ULONG                          BroadcastContextCount;
  D3DKMT_HANDLE                  BroadcastContext[D3DDDI_MAX_BROADCAST_CONTEXT];
  D3DDDI_VIDEO_PRESENT_SOURCE_ID VidPnSourceId;
  UINT                           PresentCount;
  D3DDDI_FLIPINTERVAL_TYPE       FlipInterval;
  D3DKMT_PRESENTFLAGS            Flags;
  UINT                           PresentPlaneCount;
  D3DKMT_MULTIPLANE_OVERLAY      *pPresentPlanes;
  UINT                           Duration;
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

**标志**

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
<td align="left">D3dkmthk.h</td>
</tr>
</tbody>
</table>

 

 






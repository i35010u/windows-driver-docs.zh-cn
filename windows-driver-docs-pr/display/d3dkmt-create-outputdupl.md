---
title: D3DKMT \_ 创建 \_ OUTPUTDUPL 结构
description: 了解 D3DKMT \_ CREATE \_ OUTPUTDUPL 结构，它是为系统使用而保留的。 请勿在您的驱动程序中使用。
keywords:
- D3DKMT_CREATE_OUTPUTDUPL 结构显示设备
topic_type:
- apiref
api_name:
- D3DKMT_CREATE_OUTPUTDUPL
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 613c1e871660fb8f4ebf4bf8ec3d017a3b9322e2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839637"
---
# <a name="d3dkmt_create_outputdupl-structure"></a>D3DKMT \_ 创建 \_ OUTPUTDUPL 结构


预留给系统使用。 请勿在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _D3DKMT_CREATE_OUTPUTDUPL {
  D3DKMT_HANDLE                  hAdapter;
  D3DDDI_VIDEO_PRESENT_SOURCE_ID VidPnSourceId;
  D3DKMT_HANDLE                  hSharedSurfaceGlobal;
  D3DKMT_HANDLE                  hGPUFencefaceGlobal;
  D3DKMT_HANDLE                  hKeyedMutexGlobal;
} D3DKMT_CREATE_OUTPUTDUPL;
```

<a name="members"></a>成员
-------

**hAdapter**

**VidPnSourceId**

**hSharedSurfaceGlobal**

**hGPUFencefaceGlobal**

**hKeyedMutexGlobal**

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

 

 






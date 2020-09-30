---
title: D3DKMT \_ 销毁 \_ OUTPUTDUPL 结构
description: 了解 D3DKMT \_ 销毁 \_ OUTPUTDUPL 结构，该结构保留供系统使用。 请勿在您的驱动程序中使用。
ms.assetid: ced3face-7f07-459f-8644-0062cd5db805
keywords:
- D3DKMT_DESTROY_OUTPUTDUPL 结构显示设备
topic_type:
- apiref
api_name:
- D3DKMT_DESTROY_OUTPUTDUPL
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 23b8d78c69ea9a1f27d407fe9ba883af5cdd170f
ms.sourcegitcommit: f1d6c2d0cdbecdc69ba65ed3b530755fc73c8e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91590395"
---
# <a name="d3dkmt_destroy_outputdupl-structure"></a>D3DKMT \_ 销毁 \_ OUTPUTDUPL 结构


预留给系统使用。 请勿在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _D3DKMT_DESTROY_OUTPUTDUPL {
  D3DKMT_HANDLE                  hAdapter;
  D3DDDI_VIDEO_PRESENT_SOURCE_ID VidPnSourceId;
  BOOL                           bDestroyAllContexts;
} D3DKMT_DESTROY_OUTPUTDUPL;
```

<a name="members"></a>成员
-------

**hAdapter**

**VidPnSourceId**

**bDestroyAllContexts**

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

 

 






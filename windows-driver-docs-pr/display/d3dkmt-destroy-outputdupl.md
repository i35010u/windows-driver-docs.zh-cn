---
title: D3DKMT\_DESTROY\_OUTPUTDUPL 结构
description: 保留供系统使用。 不要在您的驱动程序中使用。
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
ms.openlocfilehash: 5703b027077ec0adf5c0e782b88096529b71a065
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382949"
---
# <a name="d3dkmtdestroyoutputdupl-structure"></a>D3DKMT\_DESTROY\_OUTPUTDUPL 结构


保留供系统使用。 不要在您的驱动程序中使用。

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
<td align="left"><p>Header</p></td>
<td align="left">D3dkmthk.h （包括 D3dkmthk.h）</td>
</tr>
</tbody>
</table>

 

 






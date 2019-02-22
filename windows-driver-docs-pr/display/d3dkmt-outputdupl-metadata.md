---
title: D3DKMT\_OUTPUTDUPL\_元数据结构
description: 保留供系统使用。 不要在您的驱动程序中使用。
ms.assetid: abf4f00a-05bb-48f6-989e-f1b453fb0708
keywords:
- D3DKMT_OUTPUTDUPL_METADATA 结构显示设备
topic_type:
- apiref
api_name:
- D3DKMT_OUTPUTDUPL_METADATA
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: df6a9b410a7498c3aadc31a68435af08c19b9836
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554767"
---
# <a name="d3dkmtoutputduplmetadata-structure"></a>D3DKMT\_OUTPUTDUPL\_元数据结构


保留供系统使用。 不要在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _D3DKMT_OUTPUTDUPL_METADATA {
  D3DKMT_HANDLE                  hAdapter;
  D3DDDI_VIDEO_PRESENT_SOURCE_ID VidPnSourceId;
  D3DKMT_OUTPUTDUPL_METADATATYPE Type;
  UINT                           BufferSizeSupplied;
  PVOID                          pBuffer;
  UINT                           BufferSizeRequired;
} D3DKMT_OUTPUTDUPL_METADATA;
```

<a name="members"></a>成员
-------

**hAdapter**

**VidPnSourceId**

**Type**

**BufferSizeSupplied**

**pBuffer**

**BufferSizeRequired**

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
<td align="left">D3dkmthk.h （包括 D3dkmthk.h）</td>
</tr>
</tbody>
</table>

 

 






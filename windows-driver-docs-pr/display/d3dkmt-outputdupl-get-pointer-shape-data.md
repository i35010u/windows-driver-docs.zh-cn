---
title: D3DKMT \_ OUTPUTDUPL \_ 获取 \_ 指针 \_ 形状 \_ 数据结构
description: 了解 D3DKMT \_ OUTPUTDUPL \_ 获取 \_ 指针 \_ 形状 \_ 数据结构，该结构已保留供系统使用。 请勿在您的驱动程序中使用。
keywords:
- D3DKMT_OUTPUTDUPL_GET_POINTER_SHAPE_DATA 结构显示设备
topic_type:
- apiref
api_name:
- D3DKMT_OUTPUTDUPL_GET_POINTER_SHAPE_DATA
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3b0a62355ae9acc67f73838c710078494b9434ef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839611"
---
# <a name="d3dkmt_outputdupl_get_pointer_shape_data-structure"></a>D3DKMT \_ OUTPUTDUPL \_ 获取 \_ 指针 \_ 形状 \_ 数据结构


预留给系统使用。 请勿在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _D3DKMT_OUTPUTDUPL_GET_POINTER_SHAPE_DATA {
  D3DKMT_HANDLE                     hAdapter;
  D3DDDI_VIDEO_PRESENT_SOURCE_ID    VidPnSourceId;
  UINT                              BufferSizeSupplied;
  PVOID                             pShapeBuffer;
  UINT                              BufferSizeRequired;
  D3DKMT_OUTDUPL_POINTER_SHAPE_INFO ShapeInfo;
} D3DKMT_OUTPUTDUPL_GET_POINTER_SHAPE_DATA;
```

<a name="members"></a>成员
-------

**hAdapter**

**VidPnSourceId**

**BufferSizeSupplied**

**pShapeBuffer**

**BufferSizeRequired**

**ShapeInfo**

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

 

 






---
title: D3DDDI \_ MULTIPLANE \_ 叠加 \_ 筛选 \_ 范围结构
description: 了解 D3DDDI \_ MULTIPLANE \_ 叠加 \_ 筛选 \_ 范围结构，该结构已保留供系统使用。 不要在您的驱动程序中使用它。
ms.assetid: 61393cb5-eedc-4186-a321-703b74450ee5
keywords:
- D3DDDI_MULTIPLANE_OVERLAY_FILTER_RANGE 结构显示设备
topic_type:
- apiref
api_name:
- D3DDDI_MULTIPLANE_OVERLAY_FILTER_RANGE
api_location:
- D3dumddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 76e124ae5c483e0c16c39cd3eb060851104a681f
ms.sourcegitcommit: fc94eb0d5a41ef81c1b3ab91ad725386db0be0c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603670"
---
# <a name="d3dddi_multiplane_overlay_filter_range-structure"></a>D3DDDI \_ MULTIPLANE \_ 叠加 \_ 筛选 \_ 范围结构


预留给系统使用。 不要在您的驱动程序中使用它。

> [!NOTE]
> 此结构仅在随 windows 8) 版本8随附的 Windows 驱动程序工具包 (的 D3dumddi 标头中提供。 它已从标头的更高版本中删除。

 

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct D3DDDI_MULTIPLANE_OVERLAY_FILTER_RANGE {
  INT   Minimum;
  INT   Maximum;
  INT   Default;
  FLOAT Multiplier;
} D3DDDI_MULTIPLANE_OVERLAY_FILTER_RANGE;
```

<a name="members"></a>成员
-------

**最低**

最大值

**默认**

**乘数**

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
<td align="left">D3dumddi</td>
</tr>
</tbody>
</table>

 

 






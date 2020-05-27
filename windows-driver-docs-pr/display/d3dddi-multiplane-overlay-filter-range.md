---
title: D3DDDI \_ MULTIPLANE \_ 叠加 \_ 筛选 \_ 范围结构
description: 预留给系统使用。 不要在您的驱动程序中使用它。请注意，此结构仅在随 Windows 8 随附的 Windows 驱动程序工具包（WDK）版本8随附的 D3dumddi 标头中可用。 它已从标头的更高版本中删除。.
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
ms.openlocfilehash: 8da73872cad56eb05371dbe1a89fe358cc9eb030
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83852158"
---
# <a name="d3dddi_multiplane_overlay_filter_range-structure"></a>D3DDDI \_ MULTIPLANE \_ 叠加 \_ 筛选 \_ 范围结构


预留给系统使用。 不要在您的驱动程序中使用它。

> [!NOTE]
> 此结构仅在随 Windows 8 随附的 Windows 驱动程序工具包（WDK）版本8随附的 D3dumddi 标头中可用。 它已从标头的更高版本中删除。

 

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

**最小值**

**最大值**

**Default**

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
<td align="left"><p>Header</p></td>
<td align="left">D3dumddi</td>
</tr>
</tbody>
</table>

 

 






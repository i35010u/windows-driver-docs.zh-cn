---
title: D3DDDI \_ MULTIPLANE \_ 覆盖 \_ 筛选器结构
description: 了解 \_ \_ \_ 保留供系统使用的 D3DDDI MULTIPLANE 覆盖筛选器结构。 不要在您的驱动程序中使用它。
ms.assetid: 56276b78-5550-4d93-8a73-b1183deb54da
keywords:
- D3DDDI_MULTIPLANE_OVERLAY_FILTER 结构显示设备
topic_type:
- apiref
api_name:
- D3DDDI_MULTIPLANE_OVERLAY_FILTER
api_location:
- D3dumddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6b027d5242393460dd4b37b357c2da00a9437b72
ms.sourcegitcommit: fc94eb0d5a41ef81c1b3ab91ad725386db0be0c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603564"
---
# <a name="d3dddi_multiplane_overlay_filter-structure"></a>D3DDDI \_ MULTIPLANE \_ 覆盖 \_ 筛选器结构


预留给系统使用。 不要在您的驱动程序中使用它。

> [!NOTE]
> 此结构仅在随 windows 8) 版本8随附的 Windows 驱动程序工具包 (的 D3dumddi 标头中提供。 它已从标头的更高版本中删除。

 

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _D3DDDI_MULITPLANE_OVERLAY_FILTER {
  D3DDDI_MULTIPLANE_OVERLAY_FILTER_TYPE FilterType;
  BOOL                                  Enabled;
  INT                                   Value;
} D3DDDI_MULTIPLANE_OVERLAY_FILTER;
```

<a name="members"></a>成员
-------

**FilterType**

**已启用**

**值**

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

 

 






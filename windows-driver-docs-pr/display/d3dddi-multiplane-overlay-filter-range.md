---
title: D3DDDI\_MULTIPLANE\_覆盖\_筛选器\_范围结构
description: 保留供系统使用。 不要使用它在您的驱动程序中。请注意此结构是仅在使用 Windows Driver Kit (WDK) 8 随附版本与 Windows 8 提供的 D3dumddi.h 标头中可用。 已从更高版本的标头。 .
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
ms.openlocfilehash: c012dc263fde65fc9f23b2bb8438b0e2ee8752c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544034"
---
# <a name="d3dddimultiplaneoverlayfilterrange-structure"></a>D3DDDI\_MULTIPLANE\_覆盖\_筛选器\_范围结构


保留供系统使用。 不要使用它在您的驱动程序中。

&gt; \[!请注意\]&gt;此结构是仅在使用 Windows Driver Kit (WDK) 8 随附版本与 Windows 8 提供的 D3dumddi.h 标头中可用。 已从更高版本的标头。

 

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

**默认值**

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
<td align="left">D3dumddi.h</td>
</tr>
</tbody>
</table>

 

 






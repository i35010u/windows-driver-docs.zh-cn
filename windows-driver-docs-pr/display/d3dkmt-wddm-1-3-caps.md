---
title: D3DKMT\_WDDM\_1\_3\_CAPS 结构
description: 保留供系统使用。 不要在您的驱动程序中使用。
ms.assetid: 53DB51B2-482C-4A1D-AD03-FEB73B77F9A9
keywords:
- D3DKMT_WDDM_1_3_CAPS 结构显示设备
topic_type:
- apiref
api_name:
- D3DKMT_WDDM_1_3_CAPS
api_location:
- D3dkmdt.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6540fe640c8ff4071272774d0889ef11895abd05
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566079"
---
# <a name="d3dkmtwddm13caps-structure"></a>D3DKMT\_WDDM\_1\_3\_CAPS 结构


保留供系统使用。 不要在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _D3DKMT_WDDM_1_3_CAPS {
  union {
    struct {
      UINT SupportMiracast  :1;
      UINT IsHybridIntegratedGPU  :1;
      UINT IsHybridDiscreteGPU  :1;
      UINT SupportPowerManagementPStates  :1;
      UINT Reserved  :28;
    };
  };
} D3DKMT_WDDM_1_3_CAPS;
```

<a name="members"></a>成员
-------

**SupportMiracast**

**IsHybridIntegratedGPU**

**IsHybridDiscreteGPU**

**SupportPowerManagementPStates**

**保留**

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
<td align="left"><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">D3dkmdt.h （包括 D3dkmdt.h）</td>
</tr>
</tbody>
</table>

 

 






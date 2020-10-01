---
title: D3DKMT \_ WDDM \_ 1 \_ 3 \_ 大写字母结构
description: 了解 D3DKMT \_ WDDM \_ 1 \_ 3 \_ cap 结构，该结构保留供系统使用。 请勿在您的驱动程序中使用。
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
ms.openlocfilehash: 9f8c46780dcb674532c94e8723ae408a820cbb55
ms.sourcegitcommit: fc94eb0d5a41ef81c1b3ab91ad725386db0be0c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603619"
---
# <a name="d3dkmt_wddm_1_3_caps-structure"></a>D3DKMT \_ WDDM \_ 1 \_ 3 \_ 大写字母结构


预留给系统使用。 请勿在您的驱动程序中使用。

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

**保护**

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
<td align="left"><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">D3dkmdt (包含 D3dkmdt) </td>
</tr>
</tbody>
</table>

 

 






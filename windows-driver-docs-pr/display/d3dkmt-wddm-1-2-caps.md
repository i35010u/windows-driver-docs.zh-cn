---
title: D3DKMT\_WDDM\_1\_2\_CAPS 结构
description: 保留供系统使用。 不要在您的驱动程序中使用。
ms.assetid: 0cd26fad-4772-4631-81fc-da2ddb7dc9a1
keywords:
- D3DKMT_WDDM_1_2_CAPS 结构显示设备
topic_type:
- apiref
api_name:
- D3DKMT_WDDM_1_2_CAPS
api_location:
- D3dkmdt.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6694172357f1e9ca3a0423819e9312347bf54af8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521218"
---
# <a name="d3dkmtwddm12caps-structure"></a>D3DKMT\_WDDM\_1\_2\_CAPS 结构


保留供系统使用。 不要在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _D3DKMT_WDDM_1_2_CAPS {
  D3DKMDT_PREEMPTION_CAPS PreemptionCaps;
  union {
    struct {
      UINT SupportNonVGA  :1;
      UINT SupportSmoothRotation  :1;
      UINT SupportPerEngineTDR  :1;
      UINT SupportKernelModeCommandBuffer  :1;
      UINT SupportCCD  :1;
      UINT SupportSoftwareDeviceBitmaps  :1;
      UINT SupportGammaRamp  :1;
      UINT SupportHWCursor  :1;
      UINT SupportHWVSync  :1;
      UINT SupportSurpriseRemovalInHibernation  :1;
      UINT Reserved  :22;
    };
    UINT   Value;
  };
} D3DKMT_WDDM_1_2_CAPS;
```

<a name="members"></a>成员
-------

**PreemptionCaps**

**SupportNonVGA**

**SupportSmoothRotation**

**SupportPerEngineTDR**

**SupportKernelModeCommandBuffer**

**SupportCCD**

**SupportSoftwareDeviceBitmaps**

**SupportGammaRamp**

**SupportHWCursor**

**SupportHWVSync**

**SupportSurpriseRemovalInHibernation**

**保留**

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
<td align="left">D3dkmdt.h （包括 D3dkmdt.h）</td>
</tr>
</tbody>
</table>

 

 






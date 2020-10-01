---
title: DXGK \_ POWER \_ P \_ 状态结构
description: 了解 DXGK \_ POWER \_ P \_ 状态结构，它保留供系统使用。 不要在您的驱动程序中使用它。
ms.assetid: F4612284-36C8-49C4-914D-43C32489EABD
keywords:
- DXGK_POWER_P_STATE 结构显示设备
- PDXGK_POWER_P_STATE 结构指针显示设备
topic_type:
- apiref
api_name:
- DXGK_POWER_P_STATE
api_location:
- D3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6ed3a16941eb8dd324c7597edb854ad774fe92ec
ms.sourcegitcommit: fc94eb0d5a41ef81c1b3ab91ad725386db0be0c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603694"
---
# <a name="dxgk_power_p_state-structure"></a>DXGK \_ POWER \_ P \_ 状态结构


预留给系统使用。 不要在您的驱动程序中使用它。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_POWER_P_STATE {
  ULONG     NominalPower;
  ULONG     OperatingFrequency;
  ULONGLONG TransitionLatencies[DXGK_MAX_P_STATES];
  ULONGLONG ResidencyRequirement;
} DXGK_POWER_P_STATE, *PDXGK_POWER_P_STATE;
```

<a name="members"></a>成员
-------

**NominalPower**

**OperatingFrequency**

**TransitionLatencies**

**ResidencyRequirement**

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
<td align="left">D3dkmddi (包含 D3dkmddi) </td>
</tr>
</tbody>
</table>

 

 






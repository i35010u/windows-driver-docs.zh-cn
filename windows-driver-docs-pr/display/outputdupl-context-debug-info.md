---
title: OUTPUTDUPL\_上下文\_调试\_信息结构
description: 保留供系统使用。 不要在您的驱动程序中使用。
ms.assetid: 9b8915a2-e62e-474a-ac03-199ce6d252c2
keywords:
- OUTPUTDUPL_CONTEXT_DEBUG_INFO 结构显示设备
topic_type:
- apiref
api_name:
- OUTPUTDUPL_CONTEXT_DEBUG_INFO
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: bc91f429563af15195dd15a557f472102c518928
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540619"
---
# <a name="outputduplcontextdebuginfo-structure"></a>OUTPUTDUPL\_上下文\_调试\_信息结构


保留供系统使用。 不要在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _OUTPUTDUPL_CONTEXT_DEBUG_INFO {
  OUTPUTDUPL_CONTEXT_DEBUG_STATUS Status;
  HANDLE                          ProcessID;
  UINT32                          AccumulatedPresents;
  LARGE_INTEGER                   LastPresentTime;
  LARGE_INTEGER                   LastMouseTime;
  CHAR                            ProcessName[DXGK_DIAG_PROCESS_NAME_LENGTH];
} OUTPUTDUPL_CONTEXT_DEBUG_INFO;
```

<a name="members"></a>成员
-------

**状态**

**ProcessID**

**AccumulatedPresents**

**LastPresentTime**

**LastMouseTime**

**ProcessName**

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

 

 






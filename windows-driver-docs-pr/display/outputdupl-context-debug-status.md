---
title: OUTPUTDUPL\_上下文\_调试\_状态枚举
description: 保留供系统使用。 不要在您的驱动程序中使用。
ms.assetid: 3720b101-cac4-4f81-ae71-088ab03f8756
keywords:
- OUTPUTDUPL_CONTEXT_DEBUG_STATUS 枚举显示设备
topic_type:
- apiref
api_name:
- OUTPUTDUPL_CONTEXT_DEBUG_STATUS
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: c8ed67cc886550c192e40629defd629c82a44901
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358465"
---
# <a name="outputduplcontextdebugstatus-enumeration"></a>OUTPUTDUPL\_上下文\_调试\_状态枚举


保留供系统使用。 不要在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef enum _OUTPUTDUPL_CONTEXT_DEBUG_STATUS {
  OUTPUTDUPL_CONTEXT_DEBUG_STATUS_INACTIVE         = 0,
  OUTPUTDUPL_CONTEXT_DEBUG_STATUS_ACTIVE           = 1,
  OUTPUTDUPL_CONTEXT_DEBUG_STATUS_PENDING_DESTROY  = 2,
  OUTPUTDUPL_CONTEXT_DEBUG_STATUS_FORCE_UINT32     = 0xffffffff
} OUTPUTDUPL_CONTEXT_DEBUG_STATUS;
```

<a name="constants"></a>常量
---------

<span id="OUTPUTDUPL_CONTEXT_DEBUG_STATUS_INACTIVE"></span><span id="outputdupl_context_debug_status_inactive"></span>**OUTPUTDUPL\_CONTEXT\_DEBUG\_STATUS\_INACTIVE**

<span id="OUTPUTDUPL_CONTEXT_DEBUG_STATUS_ACTIVE"></span><span id="outputdupl_context_debug_status_active"></span>**OUTPUTDUPL\_CONTEXT\_DEBUG\_STATUS\_ACTIVE**

<span id="OUTPUTDUPL_CONTEXT_DEBUG_STATUS_PENDING_DESTROY"></span><span id="outputdupl_context_debug_status_pending_destroy"></span>**OUTPUTDUPL\_CONTEXT\_DEBUG\_STATUS\_PENDING\_DESTROY**

<span id="OUTPUTDUPL_CONTEXT_DEBUG_STATUS_FORCE_UINT32"></span><span id="outputdupl_context_debug_status_force_uint32"></span>**OUTPUTDUPL\_CONTEXT\_DEBUG\_STATUS\_FORCE\_UINT32**

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
<td align="left">D3dkmthk.h （包括 D3dkmthk.h）</td>
</tr>
</tbody>
</table>

 

 






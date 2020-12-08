---
title: OUTPUTDUPL \_ 上下文 \_ 调试 \_ 状态枚举
description: 了解 OUTPUTDUPL \_ 上下文 \_ 调试 \_ 状态枚举，该枚举保留供系统使用。 请勿在您的驱动程序中使用。
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
ms.openlocfilehash: 137b0aae2bb7271d1b834d181ed65ca17686e440
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802617"
---
# <a name="outputdupl_context_debug_status-enumeration"></a>OUTPUTDUPL \_ 上下文 \_ 调试 \_ 状态枚举


预留给系统使用。 请勿在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef enum _OUTPUTDUPL_CONTEXT_DEBUG_STATUS {
  OUTPUTDUPL_CONTEXT_DEBUG_STATUS_INACTIVE         = 0,
  OUTPUTDUPL_CONTEXT_DEBUG_STATUS_ACTIVE           = 1,
  OUTPUTDUPL_CONTEXT_DEBUG_STATUS_PENDING_DESTROY  = 2,
  OUTPUTDUPL_CONTEXT_DEBUG_STATUS_FORCE_UINT32     = 0xffffffff
} OUTPUTDUPL_CONTEXT_DEBUG_STATUS;
```

<a name="constants"></a>常量
---------

<span id="OUTPUTDUPL_CONTEXT_DEBUG_STATUS_INACTIVE"></span><span id="outputdupl_context_debug_status_inactive"></span>**OUTPUTDUPL \_ 上下文 \_ 调试 \_ 状态为 \_ 非活动**

<span id="OUTPUTDUPL_CONTEXT_DEBUG_STATUS_ACTIVE"></span><span id="outputdupl_context_debug_status_active"></span>**OUTPUTDUPL \_ 上下文 \_ 调试 \_ 状态 \_ 处于活动状态**

<span id="OUTPUTDUPL_CONTEXT_DEBUG_STATUS_PENDING_DESTROY"></span><span id="outputdupl_context_debug_status_pending_destroy"></span>**OUTPUTDUPL \_ 上下文 \_ 调试 \_ 状态 \_ 挂起 \_ 销毁**

<span id="OUTPUTDUPL_CONTEXT_DEBUG_STATUS_FORCE_UINT32"></span><span id="outputdupl_context_debug_status_force_uint32"></span>**OUTPUTDUPL \_ 上下文 \_ 调试 \_ 状态 \_ 强制 \_ UINT32**

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
<td align="left">D3dkmthk (包含 D3dkmthk) </td>
</tr>
</tbody>
</table>

 

 






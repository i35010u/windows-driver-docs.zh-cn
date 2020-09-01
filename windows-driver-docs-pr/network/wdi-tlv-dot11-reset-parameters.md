---
title: WDI_TLV_DOT11_RESET_PARAMETERS
description: WDI_TLV_DOT11_RESET_PARAMETERS 是包含 OID_WDI_TASK_DOT11_RESET 的参数的 TLV。
ms.assetid: 14F3DECD-E875-44BB-969B-705B075E4636
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_DOT11_RESET_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 949b5739b9275d4564bf64706072b4dad60c04e8
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214993"
---
# <a name="wdi_tlv_dot11_reset_parameters"></a>WDI \_ TLV \_ DOT11 \_ 重置 \_ 参数


WDI \_ tlv \_ DOT11 \_ reset \_ 参数是一个 TLV，其中包含 [OID \_ WDI \_ 任务 \_ DOT11 \_ RESET](./oid-wdi-task-dot11-reset.md)的参数。

## <a name="tlv-type"></a>TLV 类型


0xA2

## <a name="length"></a>Length


UINT8 的大小 (以字节为单位) 。

## <a name="values"></a>值


| 类型  | 说明                                                                                                     |
|-------|-----------------------------------------------------------------------------------------------------------------|
| UINT8 | 如果 (并且仅当) 此设置为1时，重置端口的所有 MIB 属性都将设置为其默认值。 |

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 


---
title: WDI_TLV_CANCEL_PARAMETERS
description: WDI_TLV_CANCEL_PARAMETERS 是包含 OID_WDI_ABORT_TASK 的参数的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CANCEL_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4e6591beddd99f1e57517f6faef90f9cfe4c819d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827465"
---
# <a name="wdi_tlv_cancel_parameters"></a>WDI \_ TLV \_ 取消 \_ 参数


WDI \_ tlv \_ CANCEL \_ 参数是一个 TLV，其中包含 [OID \_ WDI \_ ABORT \_ 任务](./oid-wdi-abort-task.md)的参数。

## <a name="tlv-type"></a>TLV 类型


0x2B

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                   | 描述                                             |
|------------------------|---------------------------------------------------------|
| NDIS \_ OID              | 指定正在中止的原始任务的 OID。 |
| UINT32                 | 指定原始任务中的事务 ID。    |
| WDI 的 \_ 端口 \_ ID (UINT16)  | 指定原始任务中的端口 ID。           |

 

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 


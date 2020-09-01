---
title: WDI_TLV_CANCEL_PARAMETERS
description: WDI_TLV_CANCEL_PARAMETERS 是包含 OID_WDI_ABORT_TASK 的参数的 TLV。
ms.assetid: 7C071743-5DF9-4CA8-873A-64B06C94388F
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CANCEL_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2a4d8b5b992c1de83dd66f5b7b8065b94056c589
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209619"
---
# <a name="wdi_tlv_cancel_parameters"></a>WDI \_ TLV \_ 取消 \_ 参数


WDI \_ tlv \_ CANCEL \_ 参数是一个 TLV，其中包含 [OID \_ WDI \_ ABORT \_ 任务](./oid-wdi-abort-task.md)的参数。

## <a name="tlv-type"></a>TLV 类型


0x2B

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                   | 说明                                             |
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 


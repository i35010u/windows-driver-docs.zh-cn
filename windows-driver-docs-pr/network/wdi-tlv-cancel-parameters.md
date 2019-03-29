---
title: WDI_TLV_CANCEL_PARAMETERS
description: WDI_TLV_CANCEL_PARAMETERS 是包含参数的 OID_WDI_ABORT_TASK TLV。
ms.assetid: 7C071743-5DF9-4CA8-873A-64B06C94388F
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CANCEL_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 904134a226fe0eccfa9d7d7cb29d586b35d91428
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568244"
---
# <a name="wditlvcancelparameters"></a>WDI\_TLV\_取消\_参数


WDI\_TLV\_取消\_参数是包含参数的 TLV [OID\_WDI\_中止\_任务](https://msdn.microsoft.com/library/windows/hardware/dn925835)。

## <a name="tlv-type"></a>TLV 类型


0x2B

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                   | 描述                                             |
|------------------------|---------------------------------------------------------|
| NDIS\_OID              | 指定从原始任务正在中止 OID。 |
| UINT32                 | 指定从原始任务的事务 ID。    |
| WDI\_端口\_ID (UINT16) | 指定从原始任务的端口 ID。           |

 

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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 





---
title: WDI_TLV_RECEIVE_COALESCING_CONFIG
description: WDI_TLV_RECEIVE_COALESCING_CONFIG 是包含 TLV 接收合并的配置。
ms.assetid: 32542203-14DE-4F91-AB85-D2FA75ECAB9E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_RECEIVE_COALESCING_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 37e47f11eceb3e22e44d3aa0f15e6187fc923a70
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382898"
---
# <a name="wditlvreceivecoalescingconfig"></a>WDI\_TLV\_RECEIVE\_COALESCING\_CONFIG


WDI\_TLV\_接收\_COALESCING\_CONFIG 是包含 TLV 接收合并的配置。

## <a name="tlv-type"></a>TLV 类型


0xDB

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                         |
|--------|---------------------------------------------------------------------|
| UINT32 | 此筛选器匹配的数据包排队到一个唯一的队列 ID。            |
| UINT32 | 具有一个介于 1 和支持的筛选器的数量的筛选器 ID。 |
| UINT32 | 最大连接延迟的毫秒数。                       |

 

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

## <a name="see-also"></a>请参阅


[OID\_WDI\_SET\_RECEIVE\_COALESCING](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-receive-coalescing)

 

 





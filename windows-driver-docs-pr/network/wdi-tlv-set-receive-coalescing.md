---
title: WDI_TLV_SET_RECEIVE_COALESCING
description: WDI_TLV_SET_RECEIVE_COALESCING 是包含接收的数据包合并参数 OID_WDI_SET_RECEIVE_COALESCING TLV。
ms.assetid: 7937517E-79E5-4BF6-9C22-79E1D73CA97C
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_SET_RECEIVE_COALESCING 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: edb89f248316ee36d9b4c4031ad99ff28566d58d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362787"
---
# <a name="wditlvsetreceivecoalescing"></a>WDI\_TLV\_SET\_RECEIVE\_COALESCING


WDI\_TLV\_设置\_接收\_COALESCING 是包含接收的数据包合并参数 TLV [OID\_WDI\_设置\_接收\_合并](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-receive-coalescing)。

## <a name="tlv-type"></a>TLV 类型


0x64

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                               | 允许多个 TLV 实例 | 可选 | 描述                                |
|------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------|
| [**WDI\_TLV\_RECEIVE\_COALESCING\_CONFIG**](wdi-tlv-receive-coalescing-config.md) |                                |          | 指定合并筛选器配置。 |
| [**WDI\_TLV\_RECEIVE\_FILTER\_FIELD**](wdi-tlv-receive-filter-field.md)           | X                              | X        | 指定的接收筛选器字段。          |

 

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

 

 





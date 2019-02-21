---
title: WDI_TLV_TCP_RSC_STATISTICS_PARAMETERS
description: WDI_TLV_TCP_RSC_STATISTICS_PARAMETERS 是 TLV OID_WDI_TCP_RSC_STATISTICS 包含 TCP RSC 统计信息。
ms.assetid: C1459DF6-6492-4C1F-A22D-2BDC6492B29C
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_TCP_RSC_STATISTICS_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 26b1b9fa0f06a91546f308e077937cdd8fa4eca0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519082"
---
# <a name="wditlvtcprscstatisticsparameters"></a>WDI\_TLV\_TCP\_RSC\_STATISTICS\_PARAMETERS


WDI\_TLV\_TCP\_RSC\_统计信息\_参数是包含 TCP RSC 的统计信息 TLV [OID\_WDI\_TCP\_RSC\_统计信息](https://msdn.microsoft.com/library/windows/hardware/dn925966)。

## <a name="tlv-type"></a>TLV 类型


0xF3

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                                                                                                                               |
|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT64 | 已合并的数据包的总数。                                                                                                                                                                                          |
| UINT64 | 已合并的字节总数。                                                                                                                                                                                            |
| UINT64 | 合并事件总数，这是已从合并的数据包格式正确的数据包总数。                                                                                                                     |
| UINT64 | RSC 的总数中止事件，这是 IP 数据报长度超出异常数。 此计数应包括其中数据包不合并由于硬件资源不足的情况。 |

 

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

 

 





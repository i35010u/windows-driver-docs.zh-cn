---
title: WDI_TLV_PACKET_FILTER_PARAMETERS
description: WDI_TLV_PACKET_FILTER_PARAMETERS 是 TLV OID_WDI_SET_RECEIVE_PACKET_FILTER 包含数据包筛选器参数。
ms.assetid: 5B26DA60-BC5D-4CC5-A620-C076CECF22C0
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PACKET_FILTER_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: dbd75422df1cb7dad11058eecd90245232412ec4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554164"
---
# <a name="wditlvpacketfilterparameters"></a>WDI\_TLV\_PACKET\_FILTER\_PARAMETERS


WDI\_TLV\_数据包\_筛选器\_参数是包含数据包筛选器参数 TLV [OID\_WDI\_设置\_接收\_数据包\_筛选器](https://msdn.microsoft.com/library/windows/hardware/dn925942)。

## <a name="tlv-type"></a>TLV 类型


0x47

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                      | 描述                                |
|---------------------------------------------------------------------------|--------------------------------------------|
| [**WDI\_PACKET\_FILTER\_TYPE**](https://msdn.microsoft.com/library/windows/hardware/dn926104) (UINT32) | 指定所需的 Wi-fi 数据包筛选器。 |

 

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

 

 





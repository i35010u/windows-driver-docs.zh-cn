---
title: WDI_TLV_P2P_CHANNEL_NUMBER
description: WDI_TLV_P2P_CHANNEL_NUMBER 是 TLV 包含 Wi-Fi Direct 频道号信息。
ms.assetid: CE17143E-5DA1-4F5B-A2E0-2BD480030129
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_CHANNEL_NUMBER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d73f64587c46f1ecbeaf9f79c477d37f9ef84597
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345951"
---
# <a name="wditlvp2pchannelnumber"></a>WDI\_TLV\_P2P\_CHANNEL\_NUMBER


WDI\_TLV\_P2P\_通道\_数是 TLV 包含 Wi-Fi Direct 频道号信息。

## <a name="tlv-type"></a>TLV 类型


0x82

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                          | 描述                                                                        |
|-------------------------------|------------------------------------------------------------------------------------|
| UINT8\[3\]                    | 国家 / 地区代码的操作的类和频道号都有效。 |
| UINT8                         | 表示频道号的运行频率类/带区。                         |
| WDI\_通道\_数 (UINT32) | 为 Wi-Fi Direct 设备或组频道号。                           |

 

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

 

 





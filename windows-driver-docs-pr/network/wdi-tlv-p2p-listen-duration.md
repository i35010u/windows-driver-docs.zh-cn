---
title: WDI_TLV_P2P_LISTEN_DURATION
description: WDI_TLV_P2P_LISTEN_DURATION 是包含 Wi-Fi Direct TLV 侦听持续时间信息。
ms.assetid: 6C14BB67-89E1-4795-9327-2B5B87BF2D7C
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_LISTEN_DURATION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 105b45d743e363ad9e4eb043a6d39a2ab41efd85
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564783"
---
# <a name="wditlvp2plistenduration"></a>WDI\_TLV\_P2P\_侦听\_持续时间


WDI\_TLV\_P2P\_侦听\_持续时间是 TLV 包含 Wi-Fi Direct 侦听持续时间信息。

## <a name="tlv-type"></a>TLV 类型


0xE9

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                                                    |
|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 持续时间，以毫秒为单位，侦听的周期。 适配器在此期间处于侦听状态。                                                           |
| UINT32 | 持续时间，以毫秒为单位，适配器应侦听周期内主动侦听。 此持续时间必须小于侦听周期持续时间。 |

 

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

 

 





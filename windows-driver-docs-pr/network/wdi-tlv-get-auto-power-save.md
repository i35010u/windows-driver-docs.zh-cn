---
title: WDI_TLV_GET_AUTO_POWER_SAVE
description: WDI_TLV_GET_AUTO_POWER_SAVE 是一个 TLV，其中包含 OID_WDI_GET_AUTO_POWER_SAVE 的自动省电信息。
ms.assetid: E57AD1CE-A252-4BB5-B983-11D3E46B7EC1
ms.date: 07/18/2017
keywords:
- WDI_TLV_GET_AUTO_POWER_SAVE 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b5c32da28f27c2f15bba41b0a8f5b9ab5ce96164
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843628"
---
# <a name="wdi_tlv_get_auto_power_save"></a>WDI\_TLV\_获取\_自动\_POWER\_保存


WDI\_TLV\_获取\_自动\_POWER\_保存是一个 TLV，其中包含 OID 的自动节能信息[\_WDI\_获取\_自动\_POWER\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-auto-power-save)。

## <a name="tlv-type"></a>TLV 类型


0xB3

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                               | 描述                                                                                                        |
|------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| UINT8                                                                              | 固件当前 AutoPSM 状态。                                                                                |
| UINT8                                                                              | 保留。                                                                                                          |
| UINT16                                                                             | 保留。                                                                                                          |
| UINT16                                                                             | 信标间隔（毫秒）。                                                                               |
| UINT8                                                                              | 以信标间隔（例如，1）表示的侦听时间间隔。                                          |
| UINT8                                                                              | 处于最低电源状态的侦听间隔（例如5）。 如果没有最新的低功率状态，则将设置为255。 |
| [**WDI\_POWER\_节省\_级别**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_power_save_level)（UINT32）              | 电源模式。                                                                                                    |
| [**WDI\_POWER\_节省\_级别**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_power_save_level)（UINT32）              | Dx 中的电源模式。                                                                                              |
| [**WDI\_POWER\_MODE\_原因\_代码**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_power_mode_reason_code)（UINT32） | 输入省/市/自治区和侦听间隔的原因。                                                  |
| UINT64                                                                             | 开始时间（毫秒）。                                                                                          |
| UINT64                                                                             | 省电模式下的毫秒数。                                                                                   |
| UINT64                                                                             | 接收到的多播数据包数，包括广播。                                                         |
| UINT64                                                                             | 已发送的多播数据包数，包括广播。                                                             |
| UINT64                                                                             | 收到的单播数据包的数量。                                                                                |
| UINT64                                                                             | 已发送的单播数据包的数量。                                                                                    |

 

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
<td><p>Windows 10</p></td>
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

 

 





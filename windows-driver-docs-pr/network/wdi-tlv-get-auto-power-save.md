---
title: WDI_TLV_GET_AUTO_POWER_SAVE
description: WDI_TLV_GET_AUTO_POWER_SAVE 是包含 OID_WDI_GET_AUTO_POWER_SAVE 自动节能信息的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_GET_AUTO_POWER_SAVE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 058f0b59a90a848a9446bcd648eb05f4921bf1cb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791315"
---
# <a name="wdi_tlv_get_auto_power_save"></a>WDI \_ TLV \_ 获取 \_ 自动 \_ 节能 \_


WDI \_ tlv \_ " \_ 自动 \_ 节能" \_ 是一种 TLV，其中包含 OID WDI 的自动节能信息，可 [ \_ \_ \_ 自动 \_ \_ 保存电源](./oid-wdi-get-auto-power-save.md)。

## <a name="tlv-type"></a>TLV 类型


0xB3

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                                                               | 描述                                                                                                        |
|------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| UINT8                                                                              | 固件当前 AutoPSM 状态。                                                                                |
| UINT8                                                                              | 保留。                                                                                                          |
| UINT16                                                                             | 保留。                                                                                                          |
| UINT16                                                                             | 信标间隔（毫秒）。                                                                               |
| UINT8                                                                              | 以信标间隔单位表示的侦听间隔 (例如，1) 。                                          |
| UINT8                                                                              | 最近一次低功耗状态的侦听间隔 (例如，5) 。 如果没有最新的低功率状态，则将设置为255。 |
| [**WDI \_POWER \_ SAVE \_ 级别**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_power_save_level) (UINT32)               | 电源模式。                                                                                                    |
| [**WDI \_POWER \_ SAVE \_ 级别**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_power_save_level) (UINT32)               | Dx 中的电源模式。                                                                                              |
| [**WDI \_电源 \_ 模式 \_ 原因 \_ 代码**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_power_mode_reason_code) (UINT32)  | 输入省/市/自治区和侦听间隔的原因。                                                  |
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

 


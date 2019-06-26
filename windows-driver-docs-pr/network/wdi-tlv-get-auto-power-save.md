---
title: WDI_TLV_GET_AUTO_POWER_SAVE
description: WDI_TLV_GET_AUTO_POWER_SAVE 是包含自动 power TLV 保存 OID_WDI_GET_AUTO_POWER_SAVE 的信息。
ms.assetid: E57AD1CE-A252-4BB5-B983-11D3E46B7EC1
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_GET_AUTO_POWER_SAVE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f325b181de800ae4ed1087d7d53042db0fddf74a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358542"
---
# <a name="wditlvgetautopowersave"></a>WDI\_TLV\_GET\_AUTO\_POWER\_SAVE


WDI\_TLV\_获取\_自动\_POWER\_另存为包含的信息的自动节能 TLV [OID\_WDI\_获取\_自动\_POWER\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-auto-power-save)。

## <a name="tlv-type"></a>TLV 类型


0xB3

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                               | 描述                                                                                                        |
|------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| UINT8                                                                              | 固件当前 AutoPSM 状态。                                                                                |
| UINT8                                                                              | 保留。                                                                                                          |
| UINT16                                                                             | 保留。                                                                                                          |
| UINT16                                                                             | 信号间隔 （毫秒）。                                                                               |
| UINT8                                                                              | 侦听间隔，在单元中的信号时间间隔 (例如，1)。                                          |
| UINT8                                                                              | 在最后一个低功耗状态 (例如，5) 侦听时间间隔。 如果没有任何最后一个低功耗状态，将设置为 255。 |
| [**WDI\_POWER\_SAVE\_LEVEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_power_save_level) (UINT32)              | 电源模式。                                                                                                    |
| [**WDI\_POWER\_SAVE\_LEVEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_power_save_level) (UINT32)              | Dx 中的电源模式。                                                                                              |
| [**WDI\_电源\_模式\_原因\_代码**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_power_mode_reason_code) (UINT32) | 进入节能状态和侦听间隔的原因。                                                  |
| UINT64                                                                             | 自启动以来的毫秒数。                                                                                          |
| UINT64                                                                             | 保存模式电源中的毫秒数。                                                                                   |
| UINT64                                                                             | 接收多路广播数据包，其中包括广播的数。                                                         |
| UINT64                                                                             | 已发送的多路广播数据包，其中包括广播的数。                                                             |
| UINT64                                                                             | 接收到的单播数据包数。                                                                                |
| UINT64                                                                             | 发送的单播数据包数。                                                                                    |

 

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

 

 





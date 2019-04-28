---
title: WDI_TLV_SEND_ACTION_FRAME_RESPONSE_PARAMETERS
description: WDI_TLV_SEND_ACTION_FRAME_RESPONSE_PARAMETERS 是包含参数的 OID_WDI_TASK_SEND_RESPONSE_ACTION_FRAME TLV。
ms.assetid: F062F8A2-EEEF-4EFC-AEC8-F1D7AB13C899
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_SEND_ACTION_FRAME_RESPONSE_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9a1855d75241425bdbd40ff113582b4bc986167a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330409"
---
# <a name="wditlvsendactionframeresponseparameters"></a>WDI\_TLV\_SEND\_ACTION\_FRAME\_RESPONSE\_PARAMETERS


WDI\_TLV\_发送\_操作\_帧\_响应\_参数是包含参数的 TLV [OID\_WDI\_任务\_发送\_响应\_操作\_帧](https://msdn.microsoft.com/library/windows/hardware/dn925962)。

## <a name="tlv-type"></a>TLV 类型


0xE2

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                                                                                                                     |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| WDI\_通道\_数 (UINT32)                     | 在 post ACK 停留时间中指定要发送操作帧和也逗留作为通道。                                    |
| WDI\_BAND\_ID (UINT32)                            | 其上发送操作帧带区的 ID。                                                                                           |
| [**WDI\_MAC\_ADDRESS**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | 目标访问的 MAC 地址点或对等互连适配器。                                                                                     |
| UINT32                                            | 发送超时。 指定最长时间 （以毫秒为单位） 发送此操作帧。                                                       |
| UINT32                                            | 后确认停留时间中。 指定的时间 （以毫秒为单位） 后确认传入数据包保留在侦听通道上。 |

 

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

 

 





---
title: WDI_TLV_P2P_DISCOVER_MODE
description: WDI_TLV_P2P_DISCOVER_MODE 是一种 TLV，其中包含 OID_WDI_TASK_P2P_DISCOVER Wi-Fi 直接发现模式信息。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_DISCOVER_MODE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 314b9d6b2a2fa13958ec6631f5fe2a3e132068da
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823705"
---
# <a name="wdi_tlv_p2p_discover_mode"></a>WDI \_ TLV \_ P2P \_ 发现 \_ 模式


WDI \_ tlv \_ P2P \_ 发现 \_ 模式是一种 Tlv，其中包含 [OID \_ WDI \_ 任务 \_ P2P \_ 探索](./oid-wdi-task-p2p-discover.md)Wi-Fi 直接发现模式信息。

## <a name="tlv-type"></a>TLV 类型


0xA9

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                                                                       | 描述                                                                                                                                                                                                                     |
|--------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_P2P \_ 发现 \_ 类型**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_discover_type) (UINT32)                     | 端口要执行的发现的类型。                                                                                                                                                                              |
| UINT8                                                                                      | 一个标志，用于指示是否需要完整的设备发现。 有效值为 0 (不需要) 和 1 (必需) 。 如果此标志设置为0，则可以执行部分发现。                                           |
| [**WDI \_P2P \_ 扫描 \_ 类型**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_scan_type) (UINT32)                             | 要由扫描阶段中的端口执行的扫描的类型。                                                                                                                                                                     |
| [**WDI \_P2P \_ 服务 \_ 发现 \_ 类型**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_service_discovery_type) (UINT32)  | 要执行的服务发现的类型。                                                                                                                                                                                  |
| UINT8                                                                                      | 扫描重复计数。 指定是否应重复执行完全扫描过程。 如果设置为0，则在主机中止任务之前，应重复扫描。                                                                 |
| UINT32                                                                                     | 扫描之间的时间。 如果扫描重复计数未设置为1，则此时间指定在完成所请求通道的完全扫描之后，) 设备应等待多长时间 (。 |

 

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

 


---
title: WDI_TLV_P2P_DISCOVER_MODE
description: WDI_TLV_P2P_DISCOVER_MODE 是一个 TLV，其中包含 OID_WDI_TASK_P2P_DISCOVER 的 Wi-fi 直接发现模式信息。
ms.assetid: 430DDDBE-C861-4E85-BFAB-31670F77696D
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_DISCOVER_MODE 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e367ef0826734593ca23562b7a4d25d5e9943b7a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840450"
---
# <a name="wdi_tlv_p2p_discover_mode"></a>WDI\_TLV\_P2P\_发现\_模式


WDI\_TLV\_P2P\_发现\_模式是一种 TLV，其中包含 OID 的 Wi-fi 直接发现模式信息[\_WDI\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-p2p-discover)\_\_

## <a name="tlv-type"></a>TLV 类型


0xA9

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                       | 描述                                                                                                                                                                                                                     |
|--------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_P2P\_发现\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_discover_type)（UINT32）                    | 端口要执行的发现的类型。                                                                                                                                                                              |
| UINT8                                                                                      | 一个标志，用于指示是否需要完整的设备发现。 有效值为0（不需要）和1（必需）。 如果此标志设置为0，则可以执行部分发现。                                           |
| [**WDI\_P2P\_扫描\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_scan_type)（UINT32）                            | 要由扫描阶段中的端口执行的扫描的类型。                                                                                                                                                                     |
| [**WDI\_P2P\_服务\_发现\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_service_discovery_type)（UINT32） | 要执行的服务发现的类型。                                                                                                                                                                                  |
| UINT8                                                                                      | 扫描重复计数。 指定是否应重复执行完全扫描过程。 如果设置为0，则在主机中止任务之前，应重复扫描。                                                                 |
| UINT32                                                                                     | 扫描之间的时间。 如果扫描重复计数未设置为1，则此时间指定在完成所请求通道的完全扫描之后，在重复扫描过程之前，设备应等待多长时间（以毫秒为单位）。 |

 

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

 

 





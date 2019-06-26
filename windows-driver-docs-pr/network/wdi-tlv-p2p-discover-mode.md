---
title: WDI_TLV_P2P_DISCOVER_MODE
description: WDI_TLV_P2P_DISCOVER_MODE 是包含 Wi-Fi Direct 发现模式信息 OID_WDI_TASK_P2P_DISCOVER TLV。
ms.assetid: 430DDDBE-C861-4E85-BFAB-31670F77696D
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_DISCOVER_MODE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cd1a69a6719e427cdab2fd9f98c092762d262408
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360729"
---
# <a name="wditlvp2pdiscovermode"></a>WDI\_TLV\_P2P\_DISCOVER\_模式


WDI\_TLV\_P2P\_DISCOVER\_模式是包含 Wi-Fi Direct 发现模式信息 TLV [OID\_WDI\_任务\_P2P\_发现](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-p2p-discover)。

## <a name="tlv-type"></a>TLV 类型


0xA9

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                       | 描述                                                                                                                                                                                                                     |
|--------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_P2P\_发现\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_p2p_discover_type) (UINT32)                    | 通过该端口执行发现的类型。                                                                                                                                                                              |
| UINT8                                                                                      | 一个标志，指示是否需要完整的设备发现。 有效值为 0 （不要求） 和 1 （必需）。 如果此标志设置为 0，可能会执行部分发现。                                           |
| [**WDI\_P2P\_SCAN\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_p2p_scan_type) (UINT32)                            | 要通过端口扫描阶段中执行的扫描类型。                                                                                                                                                                     |
| [**WDI\_P2P\_服务\_发现\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_p2p_service_discovery_type) (UINT32) | 其执行服务发现的类型。                                                                                                                                                                                  |
| UINT8                                                                                      | 扫描重复计数。 指定是否应重复的完全扫描过程。 如果设置为 0，扫描应重复进行，直到任务中止的主机。                                                                 |
| UINT32                                                                                     | 扫描之间的时间。 如果扫描重复计数未设置为 1，这次指定多长时间 （以毫秒为单位） 完成的请求的通道进行完全扫描后重复扫描过程之前应等待设备。 |

 

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

 

 





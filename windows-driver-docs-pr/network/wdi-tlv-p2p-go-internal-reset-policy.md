---
title: WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY
description: WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY 是一个 TLV，其中包含在停止/重新启动 Wi-fi 直接重置后，用于操作通道选择的固件所使用的策略。
ms.assetid: 6EA61C65-8573-491D-9268-8A02440A1175
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: caaae4ffc389879241c6ba5f9a6905d49aa5d2e8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840446"
---
# <a name="wdi_tlv_p2p_go_internal_reset_policy"></a>WDI\_TLV\_P2P\_\_内部\_重置\_策略


WDI\_TLV\_P2P\_中转\_内部\_RESET\_策略是一个 TLV，其中包含在停止/重新启动 Wi-fi Direct Reset 后，用于操作通道选择的固件所使用的策略。

## <a name="tlv-type"></a>TLV 类型


0xB2

## <a name="length"></a>长度


UINT32 的大小（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                            | 描述                                                                                                                                                                                                                                                        |
|-------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_P2P\_中转\_内部\_重置\_策略**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_go_internal_reset_policy)（UINT32） | 如果 IHV 组件自行停止/重新启动 Wi-fi 组件（例如，对于 "蓝牙归置空间流降级"），此配置将定义在重置后用于操作通道选择的固件要采用的策略。 |

 

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

 

 





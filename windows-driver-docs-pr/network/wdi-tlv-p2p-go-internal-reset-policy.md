---
title: WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY
description: WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY 是一种 TLV，其中包含在停止/重新启动 Wi-Fi 的直接重置后，用于操作通道选择的固件所使用的策略。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c1284186a9687c802078c3e37511354ac0f1081d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818807"
---
# <a name="wdi_tlv_p2p_go_internal_reset_policy"></a>WDI \_ TLV \_ P2P \_ 中转 \_ 内部 \_ 重置 \_ 策略


WDI \_ tlv \_ P2P \_ 中转 \_ 内部 \_ 重置 \_ 策略是一个 TLV，其中包含在停止/重新启动 Wi-Fi 的直接重置后，用于操作通道选择的固件所使用的策略。

## <a name="tlv-type"></a>TLV 类型


0xB2

## <a name="length"></a>长度


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型                                                                                            | 描述                                                                                                                                                                                                                                                        |
|-------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_P2P \_ 中转 \_ 内部 \_ 重置 \_ 策略**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_go_internal_reset_policy) (UINT32)  | 如果 IHV 组件在其自身的 (停止/重新启动 Wi-Fi 的直接执行重置，则为例如，对于蓝牙归置空间流降级) ，此配置将定义在重置后用于操作通道选择的固件要采用的策略。 |

 

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

 


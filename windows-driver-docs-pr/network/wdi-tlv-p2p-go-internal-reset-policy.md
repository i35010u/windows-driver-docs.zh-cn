---
title: WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY
description: WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY 是一种 TLV，其中包含在停止/重新启动 Wi-fi 直接重置后，用于操作通道选择的固件所使用的策略。
ms.assetid: 6EA61C65-8573-491D-9268-8A02440A1175
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: aec58bbfaf6fe5528d31099b7320443184d60da9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212301"
---
# <a name="wdi_tlv_p2p_go_internal_reset_policy"></a>WDI \_ TLV \_ P2P \_ 中转 \_ 内部 \_ 重置 \_ 策略


WDI \_ tlv \_ P2P \_ 中转 \_ 内部 \_ 重置 \_ 策略是一个 TLV，其中包含在停止/重新启动 wi-fi 直接重置后，用于操作通道选择的固件所使用的策略。

## <a name="tlv-type"></a>TLV 类型


0xB2

## <a name="length"></a>Length


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型                                                                                            | 说明                                                                                                                                                                                                                                                        |
|-------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_P2P \_ 中转 \_ 内部 \_ 重置 \_ 策略**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_go_internal_reset_policy) (UINT32)  | 如果 IHV 组件在其自己的 (停止/重新启动 Wi-fi 直接重置，则为例如，对于蓝牙归置空间流降级) ，此配置会定义固件在重置后用于操作通道选择的策略。 |

 

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
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 


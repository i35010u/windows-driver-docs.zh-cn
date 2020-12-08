---
title: WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT_PARAMETERS
description: WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT_PARAMETERS 是包含 Wi-Fi 直接发送操作帧结果参数的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5941cfb3fee81d6d38bfbe1e71d5935ac4bb94d1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818139"
---
# <a name="wdi_tlv_p2p_send_action_frame_result_parameters"></a>WDI \_ TLV \_ P2P \_ 发送 \_ 操作 \_ 帧 \_ 结果 \_ 参数


WDI \_ tlv \_ P2P \_ 发送 \_ 操作 \_ 帧 \_ 结果 \_ 参数是包含 Wi-Fi 直接发送操作帧结果参数的 TLV。

## <a name="tlv-type"></a>TLV 类型


0xAE

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                              | 描述                                           |
|---------------------------------------------------|-------------------------------------------------------|
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 目标 Wi-Fi Direct 设备的设备地址。 |
| UINT8                                             | 此事务的 Wi-Fi 直接对话框标记。   |

 

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

 


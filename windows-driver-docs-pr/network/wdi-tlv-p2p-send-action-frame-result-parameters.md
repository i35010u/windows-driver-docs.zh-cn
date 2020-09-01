---
title: WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT_PARAMETERS
description: WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT_PARAMETERS 是包含 Wi-fi Direct SEND Action 帧结果参数的 TLV。
ms.assetid: A0B234F2-081B-4027-9B42-76401F600707
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 34eca40d04ba46e76eaf7f5b96805e967e262e52
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211493"
---
# <a name="wdi_tlv_p2p_send_action_frame_result_parameters"></a>WDI \_ TLV \_ P2P \_ 发送 \_ 操作 \_ 帧 \_ 结果 \_ 参数


WDI \_ TLV \_ P2P \_ 发送 \_ 操作 \_ 帧 \_ 结果 \_ 参数是包含 wi-fi DIRECT send action 帧结果参数的 TLV。

## <a name="tlv-type"></a>TLV 类型


0xAE

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                              | 说明                                           |
|---------------------------------------------------|-------------------------------------------------------|
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 目标 Wi-fi Direct 设备的设备地址。 |
| UINT8                                             | 此事务的 Wi-fi Direct 对话框令牌。   |

 

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

 


---
title: WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT_PARAMETERS
description: WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT_PARAMETERS 是包含 Wi-fi Direct SEND Action 帧结果参数的 TLV。
ms.assetid: A0B234F2-081B-4027-9B42-76401F600707
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT_PARAMETERS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 76290f15188154225c5704cc6a2dacf6f81ee785
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845124"
---
# <a name="wdi_tlv_p2p_send_action_frame_result_parameters"></a>WDI\_TLV\_P2P\_发送\_操作\_帧\_结果\_参数


WDI\_TLV\_P2P\_发送\_操作\_帧\_结果\_参数是包含 Wi-fi 直接发送操作帧结果参数的 TLV。

## <a name="tlv-type"></a>TLV 类型


0xAE

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                           |
|---------------------------------------------------|-------------------------------------------------------|
| [**WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 目标 Wi-fi Direct 设备的设备地址。 |
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

 

 





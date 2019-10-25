---
title: WDI_TLV_P2P_INCOMING_FRAME_PARAMETERS
description: WDI_TLV_P2P_INCOMING_FRAME_PARAMETERS 是包含传入 Wi-fi 直接操作帧参数的 TLV。
ms.assetid: 8E530962-E4DC-4845-8A5F-87AC4E000DA8
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_INCOMING_FRAME_PARAMETERS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8569591efd1d490072287c6d3c736b902653ae25
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842763"
---
# <a name="wdi_tlv_p2p_incoming_frame_parameters"></a>WDI\_TLV\_P2P\_传入\_帧\_参数


WDI\_TLV\_P2P\_传入\_帧\_参数是包含传入 Wi-fi 直接操作帧参数的 TLV。

## <a name="tlv-type"></a>TLV 类型


0x7A

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                    | 描述                                        |
|-------------------------------------------------------------------------|----------------------------------------------------|
| [**WDI\_P2P\_操作\_帧\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_action_frame_type) | 传入操作帧的类型。             |
| [**WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)                       | 远程对等方的 MAC 地址。                |
| UINT8                                                                   | 用于事务的 Wi-fi Direct 对话框标记。 |

 

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

 

 





---
title: WDI_TLV_WAKE_PACKET_EAPOL_REQUEST_ID_MESSAGE
description: WDI_TLV_WAKE_PACKET_EAPOL_REQUEST_ID_MESSAGE 是包含 EAPOL 请求 ID 消息的 LAN 唤醒模式 ID TLV。
ms.assetid: CB898EF0-3ACF-4026-8650-91EF18E93766
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_WAKE_PACKET_EAPOL_REQUEST_ID_MESSAGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c001768bb778e609b33dfa8e5013da8b86f31a34
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542450"
---
# <a name="wditlvwakepacketeapolrequestidmessage"></a>WDI\_TLV\_WAKE\_PACKET\_EAPOL\_REQUEST\_ID\_MESSAGE


WDI\_TLV\_唤醒\_数据包\_EAPOL\_请求\_ID\_消息是包含 EAPOL 请求 ID 消息的 LAN 唤醒模式 ID TLV。

## <a name="tlv-type"></a>TLV 类型


0x5F

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                           |
|--------|---------------------------------------|
| UINT32 | 指定在 LAN 模式 id。 |

 

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

 

 





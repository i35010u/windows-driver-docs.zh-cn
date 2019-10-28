---
title: NDIS_STATUS_WWAN_CONTEXT_STATE
description: 小型端口驱动程序使用 NDIS_STATUS_WWAN_CONTEXT_STATE 通知在特定上下文的激活状态发生更改时发送事件通知。
ms.assetid: 6713f6a3-d1b7-49d0-83e1-50a33e9fff32
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_CONTEXT_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3b55732d4c213fbe96c303b05febb9d750a62ad7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842635"
---
# <a name="ndis_status_wwan_context_state"></a>\_WWAN\_上下文\_状态的 NDIS\_状态


小型端口驱动程序使用 NDIS\_状态\_WWAN\_上下文\_状态通知，以便在特定上下文的激活状态发生更改时发送事件通知。

小型端口驱动程序还可以通过此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_上下文\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state)结构。

<a name="remarks"></a>备注
-------

当上下文状态更改不是由 MB 服务的*设置*请求导致时，微型端口驱动程序还必须通知 MB 服务。 例如，如果网络停用了上下文，微型端口驱动程序必须通知 MB 服务。 微型端口驱动程序不应实现网络启动的上下文激活。

微型端口驱动程序必须直接通知 Windows 有关所有适用的上下文状态更改，如在处理 NDIS\_状态时\_WWAN\_数据包\_服务或 NDIS\_状态\_WWAN\_注册\_状态状态通知。

支持不同语音和数据连接的 MB 设备的微型端口驱动程序必须遵循以下准则：

-   在初始化时，VoiceCallState 必须设置为 WwanVoiceCallStateNone。

-   在语音呼叫开始时，发送事件通知，并将 VoiceCallState 设置为 WwanVoiceCallStateInProgress。 所有其他成员必须反映其当前状态。 如果在语音呼叫过程中没有活动连接，则应将 ConnectionId 设置为 "0"。

-   语音呼叫完成后，发送事件通知，并将 VoiceCallState 设置为 WwanVoiceCallStateHangUp。 所有其他成员必须反映其当前状态。 如果在语音呼叫挂断期间没有活动的连接，则应将 ConnectionId 设置为 "0"。 此事件完成后，必须在微型端口驱动程序中将 VoiceCallState 设置为**WwanVoiceCallStateNone** 。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_WWAN\_CONTEXT\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state)

[OID\_WWAN\_预配\_上下文](oid-wwan-provisioned-contexts.md)

 

 





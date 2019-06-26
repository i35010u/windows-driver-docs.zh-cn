---
title: NDIS_STATUS_WWAN_CONTEXT_STATE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_CONTEXT_STATE 通知的激活状态的特定上下文更改时发送事件通知。
ms.assetid: 6713f6a3-d1b7-49d0-83e1-50a33e9fff32
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_CONTEXT_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d488069c2c19d2e385ccc6a0f192a8c411698129
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382652"
---
# <a name="ndisstatuswwancontextstate"></a>NDIS\_状态\_WWAN\_上下文\_状态


微型端口驱动程序使用 NDIS\_状态\_WWAN\_上下文\_状态通知的激活状态的特定上下文更改时发送事件通知。

微型端口驱动程序还可以发送未经请求的事件与该通知。

使用此通知[ **NDIS\_WWAN\_上下文\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state)结构。

<a name="remarks"></a>备注
-------

微型端口驱动程序还必须在不为导致的上下文状态更改时通知 MB 服务*设置*来自 MB 服务请求。 例如，微型端口驱动程序必须通知 MB 服务，如果网络停用了上下文。 微型端口驱动程序不应实现网络启动上下文激活。

微型端口驱动程序必须通知 Windows 直接所有适用的上下文状态更改，如时处理 NDIS\_状态\_WWAN\_数据包\_服务或 NDIS\_状态\_WWAN\_注册\_状态状态通知。

支持单独的语音和数据连接的 MB 设备的微型端口驱动程序必须遵循以下准则：

-   在初始化时，VoiceCallState 必须设置为 WwanVoiceCallStateNone。

-   语音呼叫开始时，请使用设置为 WwanVoiceCallStateInProgress VoiceCallState 发送事件通知。 所有其他成员必须反映其当前状态。 如果语音呼叫期间没有活动连接，ConnectionId 应设置为"0"。

-   完成语音呼叫，使用设置为 WwanVoiceCallStateHangUp VoiceCallState 发送事件通知。 所有其他成员必须反映其当前状态。 对于语音呼叫挂断期间没有活动连接，ConnectionId 应设置为"0"。 此事件之后 VoiceCallState 必须设置为**WwanVoiceCallStateNone**微型端口驱动程序中。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_WWAN\_CONTEXT\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state)

[OID\_WWAN\_已设置\_上下文](oid-wwan-provisioned-contexts.md)

 

 





---
title: 数据包数据服务连接期间的语音呼叫
description: 数据包数据服务连接期间的语音呼叫
ms.assetid: 441d2fea-eb39-4af5-a8de-c288c81be99a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fc080093a852a7a6c14c0b78e2b0eb06fd2c274
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384364"
---
# <a name="voice-calls-during-packet-data-service-connections"></a>数据包数据服务连接期间的语音呼叫


下图表示微型端口驱动程序时语音呼叫位于数据包数据服务处于活动状态时应遵循的过程。 关系图使用 1xRTT 作为示例，但该过程适用于其他的无线接口。 在下图中所述的过程仅适用于返回的微型端口驱动程序**WwanVoiceClassSeparateVoiceData**中**WwanVoiceClass** OID 的响应中的成员\_WWAN\_设备\_CAPS*查询*请求。 粗体表示 OID 标识符或事务流控制中的标签和中常规文本的标签表示 OID 结构中的重要标志。

![说明微型端口驱动程序时语音呼叫位于数据包数据服务处于活动状态时应遵循的过程的关系图](images/wwanvoicecalls.png)

该过程假定接受传入的语音呼叫将提前发现任何预先存在的数据包连接。 返回的微型端口驱动程序**WwanVoiceClassSimultaneousVoiceData**中**WwanVoiceClass** OID 的响应中的成员\_WWAN\_设备\_CAP*查询*请求，当前的数据包连接应不会受到影响。

请注意，根据设计，MB 服务不支持线路声音，也不会禁止该服务。 该过程所述的以下图形应用仅当设备可以处理数据和线路声音，但只能有一次。 该过程假定语音呼叫，优先于任何潜在的预先存在的数据连接。 在这种情况下，微型端口驱动程序应挂起语音呼叫的持续时间的数据连接。 此后，微型端口驱动程序应自动重新建立 MB 连接恢复的数据服务。

若要在数据包数据服务连接过程中处理语音呼叫，使用以下过程：

1.  对于成功的数据包数据服务连接，发送微型端口驱动程序应[ **NDIS\_WWAN\_数据包\_服务\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state)到 MB 服务的通知，以指示当前 DataClass 跟[ **NDIS\_状态\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state) MB 的通知服务以指示该媒体连接状态作为**MediaConnectStateConnected**。

2.  微型端口驱动程序时放置语音呼叫或回答，应将发送[ **NDIS\_状态\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)到 MB 服务通知，以便指示媒体连接状态作为**MediaConnectStateDisconnected**。

3.  然后发送微型端口驱动程序应[ **NDIS\_状态\_WWAN\_上下文\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state)到指示MB服务通知*VoiceCall*作为设备的状态**WwanVoiceCallStateInProgress**。

4.  挂断，微型端口驱动程序应发送 NDIS\_状态\_WWAN\_上下文\_MB 服务指示的状态通知*VoiceCall* 作为设备的状态**WwanVoiceCallStateHangup**。

5.  语音调用完成后，设备将恢复数据包连接。 微型端口驱动程序应发送[ **NDIS\_状态\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)到 MB 服务通知，以便指示该媒体连接状态为**MediaConnectStateConnected**。

6.  微型端口驱动程序应发送 NDIS\_WWAN\_数据包\_服务\_，该值指示当前 DataClass MB 服务的状态通知。

 

 






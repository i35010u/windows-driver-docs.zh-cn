---
title: 数据包数据服务连接期间的语音呼叫
description: 数据包数据服务连接期间的语音呼叫
ms.assetid: 441d2fea-eb39-4af5-a8de-c288c81be99a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e4b98dcf70954f37cdf43ac4bdfbfec4ba31525
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215433"
---
# <a name="voice-calls-during-packet-data-service-connections"></a>数据包数据服务连接期间的语音呼叫


下图显示了当数据包数据服务处于活动状态时，小型端口驱动程序应遵循的过程。 此关系图使用1xRTT 作为示例，但该过程也适用于其他无线接口。 下图中所述的过程仅适用于在**WwanVoiceClass**成员中返回**WWANVOICECLASSSEPARATEVOICEDATA**以响应 OID \_ WWAN \_ 设备 \_ cap*查询*请求的微型端口驱动程序。 以粗体显示的标签表示 OID 标识符或事务流控制，而常规文本中的标签表示 OID 结构中的重要标志。

![说明当数据包数据服务处于活动状态时，当发出语音呼叫时，微型端口驱动程序应遵循的过程的关系图](images/wwanvoicecalls.png)

此过程假设接受传入的语音呼叫将预先抢占任何预先存在的数据包连接。 对于在**WwanVoiceClass**成员中返回**WWANVOICECLASSSIMULTANEOUSVOICEDATA**以响应 OID WWAN 设备 cap 查询请求的微型端口驱动程序 \_ \_ \_ ，当前数据包连接应不受影响。 *query*

请注意，在设计上，MB 服务不支持线路语音，也不会阻止该服务。 下图所示的过程仅适用于设备既可以处理数据又能处理线路，但每次只能处理一次。 此过程假定语音呼叫优先于任何可能的预先存在的数据连接。 在这种情况下，微型端口驱动程序应在语音呼叫期间暂停数据连接。 之后，小型端口驱动程序应通过重新建立 MB 连接来恢复数据服务。

若要在数据包数据服务连接过程中处理语音呼叫，请使用以下过程：

1.  对于成功的数据包数据服务连接，微型端口驱动程序应将 [**ndis \_ WWAN \_ 数据包 \_ 服务 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state) 通知发送到 Mb 服务，以指示当前 Microsoft.visualstudio.ordesigner.dataclass.，然后将 [**NDIS \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 通知发送到 mb 服务，以将媒体连接状态指示为 **MediaConnectStateConnected**。

2.  发出或应答语音呼叫时，微型端口驱动程序应将 [**NDIS \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 通知发送到 MB 服务，以将媒体连接状态指示为 **MediaConnectStateDisconnected**。

3.  然后，微型端口驱动程序应将 [**NDIS \_ 状态 \_ WWAN \_ 上下文 \_ 状态**](./ndis-status-wwan-context-state.md) 通知发送到 MB 服务，该服务将设备的 *VoiceCall* 状态指示为 **WwanVoiceCallStateInProgress**。

4.  在挂断时，微型端口驱动程序应将 NDIS \_ 状态 \_ WWAN \_ 上下文 \_ 状态通知发送到 MB 服务，该服务将设备的 *VoiceCall* 状态指示为 **WwanVoiceCallStateHangup**。

5.  在语音呼叫完成后，设备将恢复数据包连接。 微型端口驱动程序应将 [**NDIS \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 通知发送到 MB 服务，以将媒体连接状态指示为 " **MediaConnectStateConnected**"。

6.  微型端口驱动程序应将 NDIS \_ WWAN \_ 数据包 \_ 服务 \_ 状态通知发送到表示当前 microsoft.visualstudio.ordesigner.dataclass. 的 MB 服务。

 


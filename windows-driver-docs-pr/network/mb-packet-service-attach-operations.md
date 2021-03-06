---
title: MB 数据包服务操作
description: MB 数据包服务操作
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: aeabe98dbe6c883e022439730f866a62cbe8877a
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248093"
---
# <a name="mb-packet-service-operations"></a>MB 数据包服务操作

本主题介绍在数据包数据服务连接期间丢失和放弃数据包数据服务、数据包数据服务移交和语音呼叫的操作。

## <a name="losing-and-regaining-packet-data-service"></a>丢失和重新获取数据包数据服务

下图显示了在不同时间间隔内微型端口驱动程序丢失信号强度和数据包服务时应遵循的过程。 粗体标签为 OID 标识符或事务流控制。常规文本中的标签是 OID 结构中的重要标志。

![说明数据包数据服务的丢失和放弃信号的示意图](images/wwanregainingpacketdataservice.png)

若要在数据丢失后重新获得包数据服务，请使用以下过程：

1.  微型端口驱动程序将 NDIS \_ WWAN \_ 链接状态发送 \_ 到 MB 服务。

2.  微型端口驱动程序将 [**NDIS \_ WWAN \_ 信号 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state) 发送到 MB 服务。

3.  微型端口驱动程序将 [**NDIS \_ WWAN \_ 信号 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state) 发送到 MB 服务。

4.  微型端口驱动程序将 [**NDIS \_ WWAN \_ 信号 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state) 发送到 MB 服务。

5.  微型端口驱动程序将 NDIS \_ WWAN \_ 注册状态发送 \_ 到 MB 服务。

6.  微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 数据包 \_ 服务**](ndis-status-wwan-packet-service.md) 发送到 MB 服务。

7.  微型端口驱动程序将 [**NDIS \_ 状态 \_ 链接 \_ 状态**](ndis-status-link-state.md) 发送到 MB 服务。

8.  微型端口驱动程序将 [**NDIS \_ WWAN \_ 信号 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state) 发送到 MB 服务。

## <a name="packet-data-service-handoffs"></a>数据包数据服务移交

下图显示了当数据包服务在不同的基于 GSM 的技术（如 GPRS、EDGE、UMTS、HSDPA 或 TD SCDMA）之间移动时，微型端口驱动程序应遵循的步骤，或在不同 CDMA 的技术之间移动（如1xRTT、EV 或 EV-DO RevA）。 粗体标签为 OID 标识符或事务流控制。 常规文本中的标签是 OID 结构中的重要标志。

![说明包服务在不同的基于 gsm 的技术之间移动时应遵循的步骤的示意图](images/wwanpacketdataservicehandoff.png)

请注意，除非 IP 地址在移交过程中发生更改，否则，MB 服务将透明地处理移交事件，而不会中断现有连接。 但是，如果且仅当 IP 地址发生变化时，微型端口驱动程序仍必须通知 MB 服务有关媒体断开连接事件的信息。

微型端口驱动程序和他们管理的 MB 设备应该能够自动处理不同无线接口之间的第2层切换，对 MB 服务和其他覆盖应用程序的影响最小。 唯一的影响可能是对技术移交可能导致的 IP 地址的更改。 在这种情况下，微型端口驱动程序应重新建立 MB 连接，然后将数据包服务更改报告给 MB 服务。 不实现 DHCP 功能的微型端口驱动程序应使用 [IP 帮助](ip-helper.md) 程序和关联的 [功能](./ip-helper.md)。 使用 IP Helper 函数不需要实现 DHCP 功能的微型端口驱动程序。

若要交付数据包数据服务，请使用以下过程：

1.  微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 数据包 \_ 服务**](ndis-status-wwan-packet-service.md) 发送到 MB 服务。

2.  微型端口驱动程序将 NDIS \_ WWAN \_ 链接状态发送 \_ 到 MB 服务。

3.  微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 数据包 \_ 服务**](ndis-status-wwan-packet-service.md) 发送到 MB 服务。

4.  微型端口驱动程序调用具有旧 IP 地址的 [**DeleteUnicastIpAddressEntry**](/previous-versions/windows/hardware/drivers/ff546370(v=vs.85)) helper 函数

5.  微型端口驱动程序调用 [**CreateUnicastIpAddressEntry**](/previous-versions/windows/hardware/drivers/ff546227(v=vs.85)) helper 函数和新的 IP 地址

6.  微型端口驱动程序将 [**NDIS \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 发送到 MB 服务。

7.  微型端口驱动程序将 [**NDIS \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 发送到 MB 服务。

8.  微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 数据包 \_ 服务**](./ndis-status-wwan-packet-service.md) 发送到 MB 服务。

## <a name="voice-calls-during-packet-data-service-connections"></a>数据包数据服务连接期间的语音呼叫

下图显示了当数据包数据服务处于活动状态时，小型端口驱动程序应遵循的过程。 此关系图使用1xRTT 作为示例，但该过程也适用于其他无线接口。 下图中所述的过程仅适用于在 **WwanVoiceClass** 成员中返回 **WWANVOICECLASSSEPARATEVOICEDATA** 以响应 OID \_ WWAN \_ 设备 \_ cap *查询* 请求的微型端口驱动程序。 以粗体显示的标签表示 OID 标识符或事务流控制。 常规文本中的标签表示 OID 结构中的重要标志。

![说明当数据包数据服务处于活动状态时，当发出语音呼叫时，微型端口驱动程序应遵循的过程的关系图](images/wwanvoicecalls.png)

此过程假设接受传入的语音呼叫将预先抢占任何预先存在的数据包连接。 对于在 **WwanVoiceClass** 成员中返回 **WWANVOICECLASSSIMULTANEOUSVOICEDATA** 以响应 OID WWAN 设备 cap 查询请求的微型端口驱动程序 \_ \_ \_ ，当前数据包连接应不受影响。 

请注意，在设计上，MB 服务不支持线路语音，也不会阻止服务。 以上图形中所述的过程仅适用于设备既可以处理数据又能处理线路，但每次只能处理一次。 此过程假定语音呼叫优先于任何可能的预先存在的数据连接。 在这种情况下，微型端口驱动程序应在语音呼叫期间暂停数据连接。 之后，小型端口驱动程序应通过重新建立 MB 连接来恢复数据服务。

若要在数据包数据服务连接过程中处理语音呼叫，请使用以下过程：

1.  对于成功的数据包数据服务连接，微型端口驱动程序应将 [**ndis \_ WWAN \_ 数据包 \_ 服务 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state) 通知发送到 Mb 服务，以指示当前 Microsoft.visualstudio.ordesigner.dataclass.，然后将 [**NDIS \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 通知发送到 mb 服务，以将媒体连接状态指示为 **MediaConnectStateConnected**。

2.  发出或应答语音呼叫时，微型端口驱动程序应将 [**NDIS \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 通知发送到 MB 服务，以将媒体连接状态指示为 **MediaConnectStateDisconnected**。

3.  然后，微型端口驱动程序应将 [**NDIS \_ 状态 \_ WWAN \_ 上下文 \_ 状态**](./ndis-status-wwan-context-state.md) 通知发送到 MB 服务，该服务将设备的 *VoiceCall* 状态指示为 **WwanVoiceCallStateInProgress**。

4.  在挂断时，微型端口驱动程序应将 NDIS \_ 状态 \_ WWAN \_ 上下文 \_ 状态通知发送到 MB 服务，该服务将设备的 *VoiceCall* 状态指示为 **WwanVoiceCallStateHangup**。

5.  在语音呼叫完成后，设备将恢复数据包连接。 微型端口驱动程序应将 [**NDIS \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 通知发送到 MB 服务，以将媒体连接状态指示为 " **MediaConnectStateConnected**"。

6.  微型端口驱动程序应将 NDIS \_ WWAN \_ 数据包 \_ 服务 \_ 状态通知发送到表示当前 microsoft.visualstudio.ordesigner.dataclass. 的 MB 服务。

## <a name="see-also"></a>另请参阅

有关数据包服务操作的详细信息，请参阅 [OID \_ WWAN \_ 数据包 \_ 服务](oid-wwan-packet-service.md)。

 


---
title: 取消注册 SAP
description: 取消注册 SAP
keywords:
- 服务访问点 WDK CoNDIS
- Sap WDK CoNDIS
- 取消注册 Sap
- 正在注销 Sap
- 删除 Sap
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3dd47d957ec7d452c4f1252f62ff01dedc73d7a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792193"
---
# <a name="deregistering-a-sap"></a>取消注册 SAP





面向连接的客户端使用 [**NdisClDeregisterSap**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclderegistersap)注销 SAP。

下图显示了取消注册 SAP 的呼叫管理器的客户端。

![说明调用管理器的客户端注销 sap 的关系图](images/cm-04.png)

下图显示了注销 SAP 的 MCM 驱动程序的客户端。

![说明 mcm 驱动程序的客户端注销 sap 的示意图](images/fig1-04.png)

调用 **NdisClDeregisterSap** 会导致 NDIS 调用调用管理器或 MCM 驱动程序的 [**ProtocolCmDeregisterSap**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_deregister_sap) 函数。 在 *ProtocolCmDeregisterSap* 中，呼叫管理器或 MCM 驱动程序可能会与网络控制设备或其他特定于媒体的代理进行通信，以便在网络上取消注册 SAP。 此外， *ProtocolCmDeregisterSap* 必须释放为 SAP 动态分配的任何资源。

*ProtocolCmDeregisterSap* 可以同步或异步完成。 若要异步完成，调用管理器的 *ProtocolCmDeregisterSap* 函数将调用 [**NdisCmDeregisterSapComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmderegistersapcomplete)。 MCM 驱动程序的 *ProtocolCmDeregisterSap* 函数将调用 [**NdisMCmDeregisterSapComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmderegistersapcomplete)。 **Ndis (M) CmDegisterSapComplete** 通知 ndis 和客户端：调用管理器已完成其 *ProtocolCmDeregisterSap* 函数之前返回 Ndis 状态为 "挂起" 的 SAP 注销 \_ 请求 \_ 。

调用 **ndis (M) CmDeregisterSapComplete** 导致 ndis 调用客户端的 [**ProtocolClDeregisterSapComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_deregister_sap_complete) 函数。 调用 *ProtocolClDeregisterSapComplete* 表示客户端对 **NdisClDeregisterSap** 的前一调用已由调用管理器或 MCM 驱动程序处理。

请注意，客户端可以取消注册 SAP，而不会影响已在该 SAP 上收到的传入呼叫，并且不会影响该传入呼叫的 VC。

 


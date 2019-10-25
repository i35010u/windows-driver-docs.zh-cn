---
title: 注册 SAP
description: 注册 SAP
ms.assetid: 2b318bf0-4f0e-4db7-850b-510a9f2c7cf0
keywords:
- 服务访问点 WDK CoNDIS
- Sap WDK CoNDIS
- 正在注册 Sap
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed8fa8f50b6c1dbff3bbbef6fc5adb131d39d591
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842101"
---
# <a name="registering-a-sap"></a>注册 SAP





如果客户端接受传入调用，则其[**ProtocolClOpenAfCompleteEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_open_af_complete_ex)函数通常通过调用[**NdisClRegisterSap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclregistersap)向调用管理器注册一个或多个 sap。

下图显示了注册 SAP 的呼叫管理器的客户端。

![说明注册 sap 的呼叫管理器客户端的示意图](images/cm-02.png)

下图显示了注册 SAP 的 MCM 驱动程序的客户端。

![向 mcm 驱动程序注册 sap](images/fig1-02.png)

调用**NdisClRegisterSap**时，客户端请求对特定 SAP 的传入呼叫发出通知。 NDIS 将客户端提供的 SAP 信息转发到用于验证的调用管理器或 MCM 驱动程序的[**ProtocolCmRegisterSap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_reg_sap)函数。 如果给定的 SAP 已在使用中，或者如果调用管理器或 MCM 驱动程序无法识别客户端提供的 SAP 规范，则调用管理器或 MCM 驱动程序将无法执行此请求。

在*ProtocolCmRegisterSap*中，呼叫管理器或 MCM 驱动程序可能与网络控制设备或其他特定于媒体的代理进行通信，以便在面向连接的客户端的网络上注册 SAP。 *ProtocolCmRegisterSap*还存储一个表示 SAP 的 NDIS 提供的*NdisSapHandle* 。

*ProtocolCmRegisterSap*可以同步或异步完成。 若要异步完成，调用管理器的*ProtocolCmRegisterSap*函数将调用[**NdisCmRegisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmregistersapcomplete)。 MCM 驱动程序的*ProtocolCmRegisterSap*函数将调用[**NdisMCmRegisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmregistersapcomplete)。 调用**ndis （M） CmRegisterSapComplete**会使 ndis 调用客户端的[*ProtocolClRegisterSapComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_register_sap_complete)函数。

如果客户端对**NdisClRegisterSap**的调用成功，NDIS 会将 NdisSapHandle 返回给客户端，表示 SAP。

在呼叫管理器代表面向连接的客户端注册 SAP 后，它会通过调用[**NdisCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingcall)通知传入呼叫提议的客户端定向到该 sap。 MCM 驱动程序调用[**NdisMCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingcall)（请参阅[指示传入呼叫](indicating-an-incoming-call.md)）。 即使 SAP 注册仍处于挂起状态，客户端也可以在 SAP 上收到传入呼叫;也就是说，在调用其*ProtocolClRegisterSapComplete*函数之前。

 

 






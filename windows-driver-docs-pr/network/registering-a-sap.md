---
title: 注册 SAP
description: 注册 SAP
ms.assetid: 2b318bf0-4f0e-4db7-850b-510a9f2c7cf0
keywords:
- 服务访问点 WDK 的 CoNDIS
- SAPs WDK CoNDIS
- 注册 SAPs
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fff4b626a085a6361a4b26817732fcce738627d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385420"
---
# <a name="registering-a-sap"></a>注册 SAP





如果客户端接受传入的调用，其[ **ProtocolClOpenAfCompleteEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_open_af_complete_ex)函数通常注册一个或多个 SAPs 呼叫管理器通过调用[ **NdisClRegisterSap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclregistersap)。

下图显示的某调用的客户端管理器注册 SAP。

![说明注册 sap 呼叫管理器的客户端的关系图](images/cm-02.png)

下图显示了注册 SAP MCM 驱动程序的客户端。

![sap 注册 mcm 驱动程序](images/fig1-02.png)

通过调用**NdisClRegisterSap**，客户端请求的传入呼叫上特定的 SAP 的通知。 NDIS 将转发到呼叫管理器或 MCM 驱动程序的客户端提供的 SAP 信息[ **ProtocolCmRegisterSap** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cm_reg_sap)函数以进行验证。 如果给定的 SAP 已在使用或呼叫管理器或 MCM 驱动程序呼叫管理器或 MCM 驱动程序无法识别的客户端提供 SAP 规范，如果将此请求失败。

在中*ProtocolCmRegisterSap*，呼叫管理器或 MCM 驱动程序可能与网络控制设备或注册面向连接的客户端在网络上的 SAP 的其他特定于媒体的代理进行通信。 *ProtocolCmRegisterSap*还会将存储 NDIS 提供*NdisSapHandle*表示 SAP。

*ProtocolCmRegisterSap*可以同步或异步完成。 若要以异步方式完成*ProtocolCmRegisterSap*呼叫管理器的函数调用[ **NdisCmRegisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmregistersapcomplete)。 *ProtocolCmRegisterSap* MCM 驱动程序的函数调用[ **NdisMCmRegisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmregistersapcomplete)。 在调用**Ndis (M) CmRegisterSapComplete**会导致调用客户端的 NDIS [ *ProtocolClRegisterSapComplete* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_register_sap_complete)函数。

如果客户端的调用**NdisClRegisterSap**是成功，NDIS 返回到客户端表示 SAP NdisSapHandle。

呼叫管理器注册 SAP 代表的面向连接的客户端后，它将通知定向到该 SAP 通过调用传入调用产品/服务的客户端[ **NdisCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmdispatchincomingcall)。 MCM 驱动程序调用[ **NdisMCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdispatchincomingcall)(请参阅[该值指示传入调用](indicating-an-incoming-call.md))。 客户端可以接收上 SAP 的传入呼叫，甚至同时 SAP 注册仍为挂起;也就是说之前, 其*ProtocolClRegisterSapComplete*调用函数。

 

 






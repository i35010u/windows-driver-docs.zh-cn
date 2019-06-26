---
title: 取消注册 SAP
description: 取消注册 SAP
ms.assetid: 2d279348-b58e-4d7e-ac8b-211e9b8a0622
keywords:
- 服务访问点 WDK 的 CoNDIS
- SAPs WDK CoNDIS
- 取消注册的 SAPs
- 正在注销的 SAPs
- 删除 SAPs
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13cab6798f8c26fb5921f49dac0e737ae43eb8f4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384574"
---
# <a name="deregistering-a-sap"></a>取消注册 SAP





面向连接的客户端注销使用 SAP [ **NdisClDeregisterSap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclderegistersap)。

下图显示的某调用的客户端管理器取消 SAP。

![说明取消注册 sap 呼叫管理器的客户端的关系图](images/cm-04.png)

下图显示了取消 SAP MCM 驱动程序的客户端。

![说明取消注册 sap mcm 驱动程序的客户端的关系图](images/fig1-04.png)

在调用**NdisClDeregisterSap** NDIS 调用管理器的调用或 MCM 驱动程序将导致[ **ProtocolCmDeregisterSap** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cm_deregister_sap)函数。 在中*ProtocolCmDeregisterSap*，呼叫管理器或 MCM 驱动程序可能与网络控制设备或其他特定于媒体的代理能够取消注册在网络上的 SAP 通信。 此外， *ProtocolCmDeregisterSap*必须释放它动态分配适用于 SAP 的所有资源。

*ProtocolCmDeregisterSap*可以同步或异步完成。 若要以异步方式完成*ProtocolCmDeregisterSap*呼叫管理器的函数调用[ **NdisCmDeregisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmderegistersapcomplete)。 *ProtocolCmDeregisterSap* MCM 驱动程序的函数调用[ **NdisMCmDeregisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmderegistersapcomplete)。 **Ndis (M) CmDegisterSapComplete**通知 NDIS 和客户端呼叫管理器已完成其中的 SAP 注销请求其*ProtocolCmDeregisterSap*以前返回 NDIS函数\_状态\_PENDING。

调用**Ndis (M) CmDeregisterSapComplete**会导致调用客户端的 NDIS [ **ProtocolClDeregisterSapComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_deregister_sap_complete)函数。 调用*ProtocolClDeregisterSapComplete*指示客户端的之前调用**NdisClDeregisterSap**是否已处理该呼叫管理器或 MCM 驱动程序。

请注意，客户端可以取消注册 SAP 而不会影响已在 SAP 收到的传入呼叫，而不会影响该传入调用的 VC。

 

 






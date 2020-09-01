---
title: NdisXxx 函数调用的差异
description: NdisXxx 函数调用的差异
ms.assetid: 967ad913-24ca-4f05-b10b-1daa88845ed3
keywords:
- NdisCmXxx 函数 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de9935d1477a380f2fb76c8420c804aeffbb82b1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217664"
---
# <a name="differences-in-calls-to-ndisxxx-functions"></a>NdisXxx 函数调用的差异





调用管理器调用一组不同于 MCM 驱动程序的调用管理器功能。 调用管理器调用 **NdisCm_Xxx_** 函数，MCM 驱动程序调用 **NdisMCm_Xxx_** 函数。

MCM 驱动程序不调用面向连接的客户端和调用管理器都调用的 **NdisCo_Xxx_** 函数。 相反，MCM 驱动程序将调用以下可比较的 **NdisMCm_Xxx_** 函数：

-   [**NdisMCmCreateVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmcreatevc)而不是[ **NdisCoCreateVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscocreatevc)

-   [**NdisMCmDeleteVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeletevc)而不是[ **NdisCoDeleteVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscodeletevc)

-   [**NdisMCmOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmoidrequest)而不是[ **NdisCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)

-   [**NdisMCmOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmoidrequestcomplete)而不是[ **NdisCoOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequestcomplete)

MCM 驱动程序不需要与 [**NdisCoSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists)相当的呼叫，因为呼叫管理器和微型端口驱动程序之间的发送接口是 MCM 驱动程序的内部，因此不能与 NDIS 进行透明。

 


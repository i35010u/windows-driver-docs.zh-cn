---
title: 初始化的差异
description: 初始化的差异
ms.assetid: 1b19e30d-3c10-4b97-9bb4-3233f7f2a195
keywords:
- 初始化面向连接的协议
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae23a663156a747a6878d1c80568f9afcbf6d9af
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381371"
---
# <a name="differences-in-initialization"></a>初始化的差异





呼叫管理器是一种 NDIS 协议;因此，它遵循的初始化顺序对于面向连接的协议，但具有一个额外步骤。 在其[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)处理程序中，完成面向连接的协议的初始化步骤后立即呼叫管理器必须注册地址族通过调用[**NdisCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmregisteraddressfamilyex)。 在调用**NdisCmRegisterAddressFamilyEx**，在其中调用管理器注册其调用管理器函数，标识作为呼叫管理器协议。 呼叫管理器必须注册它绑定到自身的每个 NIC 的地址族。

MCM 驱动程序是一个微型端口驱动程序中;因此，它遵循通过以下步骤添加一个面向连接的微型端口驱动程序的初始化序列： MCM 驱动程序必须通过调用注册的地址族[ **NdisMCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmregisteraddressfamilyex)在其[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数后立即完成微型端口驱动程序初始化序列。 在调用**NdisMCmRegisterAddressFamilyEx**，MCM 驱动程序在其中注册其调用管理器函数，将 MCM 驱动程序与正则面向连接的微型端口驱动程序区分开来。 尽管 MCM 驱动程序注册其微型端口驱动程序的处理程序一次只能在初始化期间通过调用[ **NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)，它必须调用**NdisMCmRegisterAddressFamilyEx**所控制的每个 NIC 的一次。

 

 






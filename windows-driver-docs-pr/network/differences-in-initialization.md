---
title: 初始化的差异
description: 初始化的差异
ms.assetid: 1b19e30d-3c10-4b97-9bb4-3233f7f2a195
keywords:
- 初始化面向连接的协议
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc4aa36a3bd1eedafa415fee6b20b27a47395b60
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838140"
---
# <a name="differences-in-initialization"></a>初始化的差异





呼叫管理器是一个 NDIS 协议;因此，它遵循面向连接的协议的初始化顺序，但有一个额外的步骤。 在其[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)处理程序中，在完成面向连接的协议的初始化步骤后，调用管理器必须通过调用[**NdisCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmregisteraddressfamilyex)来注册地址族。 对**NdisCmRegisterAddressFamilyEx**的调用（在这种情况下，调用管理器注册其调用管理器函数）将该协议标识为呼叫管理器。 呼叫管理器必须为它绑定自身的每个 NIC 注册一个地址族。

MCM 驱动程序是一个微型端口驱动程序;因此，它将遵循面向连接的微型端口驱动程序的初始化序列，并添加以下步骤： MCM 驱动程序必须通过调用[**NdisMCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmregisteraddressfamilyex)中[*的MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数，在完成微型端口驱动程序初始化序列后立即进行。 对**NdisMCmRegisterAddressFamilyEx**的调用，其中 MCM 驱动程序注册其调用管理器函数，并将 MCM 驱动程序与面向连接的常规小型端口驱动程序区分开来。 尽管 MCM 驱动程序在初始化期间仅通过调用[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)来注册其微型端口驱动程序处理程序一次，但它必须对它控制的每个 NIC 调用**NdisMCmRegisterAddressFamilyEx**一次。

 

 






---
title: 初始化的差异
description: 初始化的差异
ms.assetid: 1b19e30d-3c10-4b97-9bb4-3233f7f2a195
keywords:
- 初始化面向连接的协议
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4e52663f3f90e3f7c6da25ae1a1d99f0d72f413
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379578"
---
# <a name="differences-in-initialization"></a>初始化的差异





呼叫管理器是一种 NDIS 协议;因此，它遵循的初始化顺序对于面向连接的协议，但具有一个额外步骤。 在其[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)处理程序中，完成面向连接的协议的初始化步骤后立即呼叫管理器必须注册地址族通过调用[**NdisCmRegisterAddressFamilyEx**](https://msdn.microsoft.com/library/windows/hardware/ff561685)。 在调用**NdisCmRegisterAddressFamilyEx**，在其中调用管理器注册其调用管理器函数，标识作为呼叫管理器协议。 呼叫管理器必须注册它绑定到自身的每个 NIC 的地址族。

MCM 驱动程序是一个微型端口驱动程序中;因此，它遵循通过以下步骤添加一个面向连接的微型端口驱动程序的初始化序列： MCM 驱动程序必须通过调用注册的地址族[ **NdisMCmRegisterAddressFamilyEx**](https://msdn.microsoft.com/library/windows/hardware/ff563554)在其[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数后立即完成微型端口驱动程序初始化序列。 在调用**NdisMCmRegisterAddressFamilyEx**，MCM 驱动程序在其中注册其调用管理器函数，将 MCM 驱动程序与正则面向连接的微型端口驱动程序区分开来。 尽管 MCM 驱动程序注册其微型端口驱动程序的处理程序一次只能在初始化期间通过调用[ **NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654)，它必须调用**NdisMCmRegisterAddressFamilyEx**所控制的每个 NIC 的一次。

 

 






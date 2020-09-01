---
title: Winsock 内核简介
description: Winsock 内核简介
ms.assetid: 52c65b9f-e3b3-4b0d-8334-7db1abb2c971
keywords:
- Winsock 内核 WDK 网络，关于 Winsock 内核
- WSK WDK 网络，关于 Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d13f655dfc074f1d5a5445f0ba7c09f57bf964e2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212893"
---
# <a name="introduction-to-winsock-kernel"></a>Winsock 内核简介


Winsock 内核 (WSK) 是 [ (NPI) 的内核模式网络编程接口 ](network-programming-interface.md)。 使用 WSK，内核模式软件模块可以使用用户模式 Winsock2 支持的相同套接字编程概念执行网络 i/o 操作。 WSK NPI 支持熟悉的套接字操作，例如套接字创建、绑定、连接建立和数据传输 (发送和接收) 。 然而，虽然 WSK NPI 支持与用户模式 Winsock2 的大部分相同的套接字编程概念，但它是一个全新的、不同的接口，它具有独特的特性（如使用 Irp 和事件回调的异步 i/o）来提高性能。

面向 Windows Vista 和更高版本 Microsoft Windows 的内核模式网络模块应该使用 WSK，而不是 [TDI](/previous-versions/windows/hardware/network/ff565094(v=vs.85)) ，因为 WSK 提供改进的性能和编程。 筛选器驱动程序应在 Windows Vista 上实现 [Windows 筛选平台](introduction-to-windows-filtering-platform-callout-drivers.md) ，而 TDI 客户端应实现 WSK。

**注意**   Windows Vista 之后的 Microsoft Windows 版本不支持 TDI。 请改用 [Windows 筛选平台](windows-filtering-platform-callout-drivers2.md) 或 [Winsock 内核](/windows-hardware/drivers/ddi/_netvista/) 。

 

 


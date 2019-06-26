---
title: Winsock 内核简介
description: Winsock 内核简介
ms.assetid: 52c65b9f-e3b3-4b0d-8334-7db1abb2c971
keywords:
- Winsock 内核 WDK 网络、 有关 Winsock 内核
- WSK WDK 网络、 有关 Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d516cde9492582778576a1ce51dee676ee814e31
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386338"
---
# <a name="introduction-to-winsock-kernel"></a>Winsock 内核简介


Winsock Kernel (WSK) 是内核模式[网络编程接口 (NPI)](network-programming-interface.md)。 使用 WSK，内核模式软件模块可以执行网络 I/O 操作使用相同的套接字编程支持的用户模式下 Winsock2 的概念。 WSK NPI 支持创建套接字、 绑定、 建立连接，数据传输等熟悉的套接字操作 （发送和接收）。 但是，尽管 WSK NPI 支持大多数相同的套接字作为用户模式下 Winsock2 编程概念，它是具有唯一特征，例如使用 Irp 和事件的回调来提高性能的异步 I/O 的完全新功能和不同的接口。

内核模式网络模块用于 Windows Vista 和更高版本的 Microsoft Windows 应使用而不是 WSK [TDI](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565094(v=vs.85))因为 WSK 提供改进的性能和方便简化编程。 筛选器驱动程序应实现[Windows 筛选平台](introduction-to-windows-filtering-platform-callout-drivers.md)客户端应在 Windows Vista 和 TDI 实现 WSK。

**请注意**  TDI 将不支持在 Microsoft Windows 版本在 Windows Vista 后。 使用[Windows 筛选平台](windows-filtering-platform-callout-drivers2.md)或[Winsock 内核](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)相反。

 

 

 






---
title: Winsock 内核扩展接口
description: Winsock 内核扩展接口
keywords:
- Winsock 内核 WDK 网络，扩展接口
- WSK WDK 网络，扩展接口
- 扩展接口 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a686ed911a1666463a1f748777aa749d7c485151
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836237"
---
# <a name="winsock-kernel-extension-interfaces"></a>Winsock 内核扩展接口


Winsock 内核 (WSK) [网络编程接口 (NPI)](network-programming-interface.md) 支持 *扩展接口*。 WSK 子系统可以使用扩展接口将 WSK 套接字的功能扩展到目前由 WSK NPI 定义的一组套接字函数和事件回调函数之外。 每个扩展接口都由与 WSK NPI 无关的 NPI 定义。 当前尚未定义扩展接口。

WSK 应用程序可以通过使用 [**SIO \_ WSK \_ register \_ extension**](./sio-wsk-register-extension.md) 套接字 IOCTL 操作来注册 WSK 子系统支持的扩展接口。 WSK 应用程序在套接字基础上注册扩展接口。

有关注册扩展接口的详细信息，请参阅 [注册扩展接口](registering-an-extension-interface.md)。

 


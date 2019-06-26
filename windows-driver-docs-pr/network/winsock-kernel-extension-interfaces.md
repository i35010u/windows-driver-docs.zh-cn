---
title: Winsock 内核扩展接口
description: Winsock 内核扩展接口
ms.assetid: db0030fa-0ee9-482b-b6ba-e95b40a25473
keywords:
- 网络、 Winsock 内核 WDK 扩展插件接口
- WSK WDK 网络、 扩展插件接口
- 扩展接口 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22d75375e7bd45b526d71ac201af3c02e1cc18df
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360211"
---
# <a name="winsock-kernel-extension-interfaces"></a>Winsock 内核扩展接口


Winsock Kernel (WSK)[网络编程接口 (NPI)](network-programming-interface.md)包括对支持*扩展插件接口*。 WSK 子系统可以使用扩展插件接口来扩展 WSK 之外的一套接字函数和由 WSK NPI 当前定义的事件回调函数的套接字功能。 由独立于 WSK NPI NPI 定义每个扩展接口。 当前已不定义任何扩展插件接口。

WSK 应用程序可以注册一个扩展接口以使用支持的 WSK 子系统[ **SIO\_WSK\_注册\_扩展**](https://docs.microsoft.com/windows-hardware/drivers/network/sio-wsk-register-extension)套接字IOCTL 操作。 WSK 应用程序注册为基于套接字的套接字的扩展插件接口。

有关注册的扩展接口的详细信息，请参阅[注册一个扩展接口](registering-an-extension-interface.md)。

 

 






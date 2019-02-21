---
title: Winsock 内核扩展插件接口
description: Winsock 内核扩展插件接口
ms.assetid: db0030fa-0ee9-482b-b6ba-e95b40a25473
keywords:
- 网络、 Winsock 内核 WDK 扩展插件接口
- WSK WDK 网络、 扩展插件接口
- 扩展接口 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45126db08fc387f48b798fceead8807cf28d1f60
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521953"
---
# <a name="winsock-kernel-extension-interfaces"></a>Winsock 内核扩展插件接口


Winsock Kernel (WSK)[网络编程接口 (NPI)](network-programming-interface.md)包括对支持*扩展插件接口*。 WSK 子系统可以使用扩展插件接口来扩展 WSK 之外的一套接字函数和由 WSK NPI 当前定义的事件回调函数的套接字功能。 由独立于 WSK NPI NPI 定义每个扩展接口。 当前已不定义任何扩展插件接口。

WSK 应用程序可以注册一个扩展接口以使用支持的 WSK 子系统[ **SIO\_WSK\_注册\_扩展**](https://msdn.microsoft.com/library/windows/hardware/ff570819)套接字IOCTL 操作。 WSK 应用程序注册为基于套接字的套接字的扩展插件接口。

有关注册的扩展接口的详细信息，请参阅[注册一个扩展接口](registering-an-extension-interface.md)。

 

 






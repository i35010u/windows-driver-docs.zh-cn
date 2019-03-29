---
title: 后台处理程序通知的术语
description: 后台处理程序通知的术语
ms.assetid: 7d4888b1-cb5f-4095-9e1b-c330c04e4971
keywords:
- 后台处理程序通知 WDK 打印，术语
- 打印后台处理程序通知 WDK，术语
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6c9f5a261b823b162460533b45e73645c64d449
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561984"
---
# <a name="spooler-notification-terminology"></a>后台处理程序通知的术语





Asnychronous 后台处理程序通知的讨论中使用以下术语。

<a href="" id="callback-interface"></a>回调接口  
当侦听客户端注册通知时，它必须提供一个指向[IPrintAsyncNotifyCallback](https://go.microsoft.com/fwlink/p/?linkid=124755)接口，如本文档后面所述。 通知到达时或当通道关闭时调用此接口的方法。

<a href="" id="listening-clients-"></a>侦听客户端   
是指应用程序或注册以接收打印通知的后台处理程序内部组件。 这是不同于什么以前称为后台处理程序通知管道的客户端。 后台处理程序通知管道的客户端是任何组件定义通知类型和架构。

<a href="" id="notification"></a>通知  
通过通知通道打印组件和侦听客户端之间发送数据。

<a href="" id="notification-channel-"></a>通知通道   
一个逻辑组件。 表示由**IPrintAsyncNotifyCallback**接口指针，如本文档后面所述。

打印组件需要发送通知时创建通知通道。 侦听客户端发送到打印组件时将使用通知通道。

<a href="" id="notification-registration-handle"></a>通知注册句柄  
创建时由服务侦听客户端的句柄注册接收通知。 侦听客户端可以使用此句柄来取消注册通知。

<a href="" id="printing-component"></a>打印组件  
表示组件 Spoolsv.exe，如打印处理器、 加载驱动程序，并监视。

<a href="" id="service"></a>service  
是指由后台处理程序，作为服务本身 (Spoolsv.exe) 的一部分或作为客户端 (Winspool.drv) 的一部分实现的功能。

 

 





---
title: USB 远程 NDIS 概述
description: USB 远程 NDIS 概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6565c2256f4bf9f973a115edbdbea54be02ca61
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815917"
---
# <a name="usb-remote-ndis-overview"></a>USB 远程 NDIS 概述




USB 远程 NDIS 设备作为 USB 通信设备类实现 (具有两个接口的 CDC) 设备。 一个通信类接口，类型为抽象控件，一个数据类接口组合在一起形成一个功能单元，表示 USB 远程 NDIS 设备。 通信类接口包含事件通知的单个终结点，并使用控制消息的共享双向控制终结点。 数据类接口包括两个用于数据流量的批量终结点。

>[!NOTE]
> 需要了解通用串行总线 (USB) 规范版本1.1 和2.0。 建议将 USB 通信设备类 (CDC) 规范作为参考。 可以在中找到这些文档 https://www.usb.org 。

 

 

 






---
title: USB 远程 NDIS 概述
description: USB 远程 NDIS 概述
ms.assetid: 05714f49-38bc-4a36-83db-2eeb16c6add6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d87b336dacf5b2412b144897acc0ae4b2a8fdb2f
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210757"
---
# <a name="usb-remote-ndis-overview"></a>USB 远程 NDIS 概述




USB 远程 NDIS 设备作为带有两个接口的 USB 通信设备类（CDC）设备实现。 一个通信类接口，类型为抽象控件，一个数据类接口组合在一起形成一个功能单元，表示 USB 远程 NDIS 设备。 通信类接口包含事件通知的单个终结点，并使用控制消息的共享双向控制终结点。 数据类接口包括两个用于数据流量的批量终结点。

>[!NOTE]
> 了解通用串行总线（USB）规范版本1.1 和2.0 是必需的。 建议将 USB 通信设备类（CDC）规范作为参考。 这些文档，请参阅 [http://www.usb.org](https://www.usb.org)。

 

 

 






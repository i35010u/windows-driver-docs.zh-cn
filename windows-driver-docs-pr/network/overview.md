---
title: USB 远程 NDIS 概述
description: USB 远程 NDIS 概述
ms.assetid: 05714f49-38bc-4a36-83db-2eeb16c6add6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd33595210dd61bb4c83a6ca784f70b836887e1a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340005"
---
# <a name="usb-remote-ndis-overview"></a>USB 远程 NDIS 概述




USB 远程 NDIS 设备实现为具有两个接口的 USB 通信设备类 (CDC) 设备。 抽象控件类型的通信类接口和数据类接口结合起来以形成单个功能单元表示 USB 远程 NDIS 设备。 通信类接口包括用于事件通知的单个终结点，并将共享的双向控制终结点的控制消息。 数据类接口包括用于数据流量的两个大容量终结点。

>[!NOTE]
> 通用串行总线 (USB) 规范版本 1.1 和 2.0 的了解是必需的。 USB 通信设备类 (CDC) 规范建议作为引用。 这些文档，请参阅 [http://www.usb.org](http://www.usb.org )。

 

 

 






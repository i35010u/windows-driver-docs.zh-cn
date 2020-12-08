---
title: 连接到 IEEE 1284.3 数据链路设备
description: 连接到 IEEE 1284.3 数据链路设备
keywords:
- 并行端口 WDK、IEEE 1284 设备
- IEEE 1284 WDK
- 数据链接服务支持 WDK 并行端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfe776e2da8d778cee59debb6cee8ad98694bb6e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812643"
---
# <a name="connecting-to-an-ieee-12843-data-link-device"></a>连接到 IEEE 1284.3 数据链路设备





系统提供的并行端口函数驱动程序不提供对 IEEE 1284.3 数据链路层服务的完全支持;但是，它提供了内部设备控制请求，上层驱动程序可以使用这些请求来连接、断开、重置和通知 IEEE 1284.3 数据链接设备。 这些服务正在开发中，旨在支持未正式提供的新设备。 有关 IEEE 1284.3 数据链接服务支持的详细信息，请参阅 Microsoft Windows 驱动程序开发工具包 (DDK) 中的示例代码 *\\ src \\ 内核 \\ parport* 。  (在 Windows 驱动程序工具包 WDK 之前的 DDK \[ \] 。 ) 

 

 





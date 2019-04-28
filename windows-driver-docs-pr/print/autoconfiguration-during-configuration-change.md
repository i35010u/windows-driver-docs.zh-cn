---
title: 配置更改期间的自动配置
description: 配置更改期间的自动配置
ms.assetid: 0294d34d-06e4-4e57-8f4d-4100ab482852
keywords:
- 自动配置 WDK 打印机，在配置更改
- 打印机自动配置 WDK 打印机，在配置更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7a9df7b0b9aa67cc82eaaea6b7802002f57f7f6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350777"
---
# <a name="autoconfiguration-during-configuration-change"></a>配置更改期间的自动配置


安装该设备后，端口监视器负责配置数据保持为最新的通过将事件发送或轮询。 每当驱动程序或应用程序感兴趣的设备的当前配置，它可以使用[bidi 通信接口](https://msdn.microsoft.com/library/windows/hardware/ff545163)并[bidi 通信架构](https://msdn.microsoft.com/library/windows/hardware/ff545175)若要查询的端口监视器此信息。

下图显示数据流中自动配置，当设备的配置更改时：

![说明当设备的配置更改时自动配置中的数据流关系图](images/autocfgcfgchange.png)

1.  该设备的配置更改时，设备使用 Web 服务事件 （WS 事件） 协议将通知打印子系统，其状态已更改，但不描述特定更改。 标准 TCP/IP 端口监视器将轮询设备不支持 WS 事件。

2.  端口监视器生成的通知设备配置已更改，并将通知发送到后台处理程序。

3.  后台处理程序将通知发送到该驱动程序，通过调用`DrvPrinterEvent`并传递打印机\_事件\_配置\_的调用中更新。 此函数调用可用于通知的设备的配置已更改的驱动程序。

驱动程序可以确定该设备，配置中的更改时，因为通知消息传送的更改 （Bidi 通知设计规范中定义了架构） 的值。 但是，如果太大，无法通过的通知机制发送通知，通知将具有一个或多个 ReducedSchema 实例，每个这指示已更改设备特征，但没有它的新值的任何详细信息。

 

 





---
title: AV/C 内核接口和流式处理代理插件
description: 提供有关 AV/C 内核流式处理接口和内核流式处理代理插件的信息
keywords:
- 内核流接口 WDK AV/C
- 内核流式处理代理插件 WDK AV/C
- AV/C WDK，内核流式处理代理插件
- AV/C WDK，内核流式处理接口
- 代理插件 WDK AV/C
- 内核流式处理代理 WDK AVStream
- KS 代理 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb6d9d5e03711a860904062bf6273fb4197abd22
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834007"
---
# <a name="avc-kernel-streaming-interface-and-kernel-streaming-proxy-plug-ins"></a>AV/C 内核-流式处理接口和内核流式处理代理插件



供应商应该将对等互连驱动程序和/或虚拟子单位驱动程序编写为使用 Stream 类接口 (内核流式处理1.0 的 WDM 驱动程序，该驱动程序在文件 *Stream.sys*) 或在文件 *Ks.sys*) 中实现的 AVStream 接口 (内核流式处理2.0。 AVStream 是首选接口，因为 stream 类接口已过时，Microsoft 不再对其进行任何进一步的开发。

使用任一接口的子单位驱动程序甚至可以共存于同一 AV/C 单元中。 例如，如果子单位驱动程序使用 AVStream，则子单位驱动程序将布局与子单位的 pin 和筛选器描述符相对应的静态结构。 然后，次级驱动程序通过调用 [**KsInitializeDriver**](/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver) AVStream 函数向 AVStream 注册。 有关这两个接口中使用的概念的详细信息，请参阅 [内核流式处理](kernel-streaming.md)。 有关 AVStream 的详细信息，请参阅 [AVStream 概述](avstream-overview.md)。 有关 Stream 类的详细信息，请参阅 [流式处理微型驱动程序](/windows-hardware/drivers/ddi/_stream/index)。

内核流式处理接口提供的标准机制与应用程序用来与子单位驱动程序交互并控制该驱动程序。 在应用程序级别控制 AV/C 子单元连接的建议方法是使用 Microsoft DirectShow 筛选器和筛选器图。 DirectShow 的内核流式处理 (KS) 代理机制提供了一个 (*ksproxy.ax*) 的通用筛选器，该筛选器可实现一种标准方式来表示次级的属性，并提供一种标准方式来表示次级单位可能触发的事件。 在 AV/C 子单位驱动程序中实现支持相关的 KS 属性和事件所需的代码。 有关表示次级属性的详细信息，请参阅 [内核流式处理属性集](./avstream-property-sets.md)。 有关表示次级事件的详细信息，请参阅 [内核流式处理事件集](./kernel-streaming-event-sets.md)。

可以使用由 Microsoft 或供应商提供的代理插件来扩展 KS 代理筛选器。 通过扩展 KS 代理筛选器，COM 接口可以隐藏 KS 属性和事件集的低级别详细信息。 你需要将插件与你的子单位驱动程序关联到设备的 INF 文件中。

直接访问属性和事件集的一般方法仍可用。 用于磁带子单元连接) 的 **IAMExtTransport** 接口 (是在代理插件中实现的接口示例。 此插件还可以包含提供用户界面以控制设备的属性页。 这些属性页通常用于测试目的，而不是用于最终用户设备交互。 可以使用 GraphEdit 或 AMCap 实用程序来测试插件的 KS 属性。 WDK 和 Windows SDK 都包含这些实用程序。


---
title: AV/C 内核接口和流式处理代理插件
description: 介绍有关 AV/C 内核流式处理接口和内核流式处理代理插件
ms.assetid: 0831d917-5afc-4c0c-832a-c2b2669b8c22
keywords:
- 内核流式处理接口 WDK AV/C
- 内核流式处理代理插件 WDK AV/C
- AV/C WDK，内核流式处理代理插件
- AV/C WDK，内核流式处理接口
- 代理插件 WDK AV/C
- 内核流式处理代理 WDK AVStream
- KS 代理 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aac8a33428b49fb14c4b7c8cb3f5e659bc078e86
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576122"
---
# <a name="avc-kernel-streaming-interface-and-kernel-streaming-proxy-plug-ins"></a>AV/C 内核流式处理接口和内核流式处理代理插件



供应商应将对等方和/或虚拟子单元驱动程序编写为使用 Stream 类接口的 WDM 驱动程序 (内核流式处理 1.0，它在文件中实现*Stream.sys*) 或 AVStream 接口 (内核流式处理 2.0，这在文件中实现*Ks.sys*)。 AVStream 是首选的接口，因为流类接口已过时，Microsoft 已停止使用它的任何进一步开发。

使用任一接口的子单元驱动程序可以共存，即使在相同的 AV/C 单元中。 例如，如果子单元驱动程序使用 AVStream，子单元驱动程序将以对应于子单元的 pin 和筛选器描述符的静态结构布局。 子单元驱动程序然后将注册到 AVStream 通过调用[ **KsInitializeDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff562683) AVStream 函数。 在这两个接口中使用的概念的详细信息，请参阅[内核流式处理](kernel-streaming.md)。 有关 AVStream 详细信息，请参阅[AVStream 概述](avstream-overview.md)。 Stream 类的详细信息，请参阅[流式处理微型驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff568275)。

任一内核流式处理接口提供了相同的标准机制，应用程序用来与之交互和控制子单元驱动程序。 建议的方法来控制应用程序级别的 AV/C 子单元连接是通过 Microsoft DirectShow 筛选器和筛选器关系图。 流式处理 (KS) 代理机制的 DirectShow 内核提供了通用的筛选器 (*ksproxy.ax*) 这样的标准方法来表示的子单元属性以及的标准方式来表示子单元可能的事件触发器。 在实现 AV/C 子单元驱动程序中支持的相关 KS 属性和事件所需的代码。 表示子单元属性的详细信息，请参阅[内核流式处理的属性集](https://msdn.microsoft.com/library/windows/hardware/ff554246)。 表示子单元事件的详细信息，请参阅[内核流式处理的事件集](https://msdn.microsoft.com/library/windows/hardware/ff560847)。

可以使用代理插件，提供由 Microsoft 或供应商扩展 KS 代理筛选器。 扩展 KS 代理筛选器允许 COM 接口，若要隐藏的 KS 属性和事件集的低级别详细信息。 您对您设备的 INF 文件中的子单元驱动程序关联的插件。

用于直接访问的属性和事件的常规方法设置仍然可用。 **IAMExtTransport** （用于磁带子单元连接） 的接口是在代理插件中实现的接口的示例。 该插件还可以包括提供了用于控制设备的用户界面的属性页。 出于测试目的，而不是最终用户设备交互通常使用这些属性页。 GraphEdit 或 AMCap 实用程序可用于测试的即插即用接 KS 属性。 WDK 和 Windows SDK 中包含这些实用程序。

 






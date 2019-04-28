---
title: 内核流式处理代理插件设计指南
description: 内核流式处理代理插件设计指南
ms.assetid: 9a2b83ab-f54c-421b-bc9b-7dad63cd8cb5
keywords:
- 内核流式处理代理 WDK AVStream 插件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e291b4ff1da8cbf70d69c1c29457e00b8fb3b23b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341207"
---
# <a name="kernel-streaming-proxy-plug-ins-design-guide"></a>内核流式处理代理插件设计指南


内核流式处理 (KS) 代理模块 (*Ksproxy.ax*) 是在内核模式和用户模式应用程序中的中转站 KS 之间的通信的 DirectShow 筛选器对象。 用户模式组件可使用 KS 代理与依赖于使用任何微型驱动程序进行通信*Ks.sys*。

具体而言，应用程序可以使用 KS 代理模块来控制和从 KS KS 微型驱动程序实现的对象中检索信息。 KS 对象包括，例如，KS 筛选器、 KS 插针和 KS 时钟。

您可以扩展 KS 代理通过编写一个插件，这是一个 COM 接口，提供了用于访问属性值的方法。 插件模型的一个优点是，它提供了一种机制，比起直接使用 KS pin 和 KS 更熟悉使用的应用程序编写器筛选的属性集。

以下部分提供如何编写插件的界面处理程序或使用 KS 代理通信使用基于 KS 的微型驱动程序的属性页的高级说明。

插件的接口提供了以编程方式控制来获取和设置应用程序中的属性值。 或者，如果你的目标是使用户能够控制通过用户界面的属性，属性页更有意义。 这两种机制需要更新注册表。

[注册 KS 代理插件](registering-ks-proxy-plug-ins.md)

[接口处理程序插件](interface-handler-plug-in.md)

[插件的属性页](property-page-plug-in.md)

有关 KS 代理 COM 接口、 导出的帮助器函数和由应用程序和插件的结构的详细信息，请参阅[内核流式处理代理](https://msdn.microsoft.com/library/windows/hardware/ff560877)。

 

 





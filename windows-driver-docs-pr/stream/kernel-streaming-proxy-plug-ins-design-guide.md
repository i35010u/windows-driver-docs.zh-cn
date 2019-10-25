---
title: 内核流式处理代理插件设计指南
description: 内核流式处理代理插件设计指南
ms.assetid: 9a2b83ab-f54c-421b-bc9b-7dad63cd8cb5
keywords:
- 内核流式处理代理 WDK AVStream，插件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dec4a8b8641b6b7df567babb0f6f9f85c7f7657e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845562"
---
# <a name="kernel-streaming-proxy-plug-ins-design-guide"></a>内核流式处理代理插件设计指南


内核流式处理（KS）代理模块（*Ksproxy.ax*）是一个 DirectShow 筛选器，它在内核模式和用户模式应用程序中的 KS 对象之间进行通信。 用户模式组件可以使用 KS 代理与基于*KS*的任何微型驱动程序进行通信。

具体而言，应用程序可以使用 KS 代理模块来控制和检索 KS 微型驱动程序实现的 KS 对象的信息。 KS 对象包括： KS 筛选器、KS 插针和 KS 时钟。

您可以通过编写插件来扩展 KS 代理，该插件是提供访问属性值的方法的 COM 接口。 插件模型的优点是，它为应用程序编写器提供的机制比直接使用 KS pin 和 KS 筛选器属性集更熟悉。

以下各节提供了有关如何编写接口处理程序插件或使用 KS 代理与基于 KS 的微型驱动程序通信的属性页的高级说明。

接口插件提供用于从应用程序中获取和设置属性值的编程控件。 或者，如果您的目标是使用户能够通过用户界面操作属性，则属性页会更有意义。 这两种机制都需要更新注册表。

[注册 KS 代理插件](registering-ks-proxy-plug-ins.md)

[接口处理程序插件](interface-handler-plug-in.md)

[属性页插件](property-page-plug-in.md)

有关应用程序和插件使用的 KS 代理 COM 接口、已导出的帮助器函数和结构的详细信息，请参阅[内核流式处理代理](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)。

 

 





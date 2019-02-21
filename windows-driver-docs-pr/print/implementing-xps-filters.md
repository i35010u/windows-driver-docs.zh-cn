---
title: 实现 XPS 筛选器
description: 实现 XPS 筛选器
ms.assetid: 681f533f-d6f6-43a3-be0b-10d8c1a6f12e
keywords:
- XPSDrv 的打印机驱动程序 WDK，呈现模块
- 呈现模块 WDK XPSDrv XPS 筛选器
- XPS 筛选 WDK XPSDrv
- WDK XPS 的筛选器
- IPrintPipelineFilter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4b444e04e45231277c96e6798ea0bd3938e25ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547829"
---
# <a name="implementing-xps-filters"></a>实现 XPS 筛选器


XPS 的所有筛选器必须实现[IPrintPipelineFilter](https://msdn.microsoft.com/library/windows/hardware/ff554286)接口。

在调用[ **IPrintPipelineFilter::InitializeFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff554291)方法中，筛选器应：

1.  缓存到指针[IPrintPipelineManagerControl](https://msdn.microsoft.com/library/windows/hardware/ff554303)接口。

2.  处理中的相关数据[IPrintPipelinePropertyBag](https://msdn.microsoft.com/library/windows/hardware/ff554320)接口。

3.  调用[ **IInterFilterCommunicator::RequestReader** ](https://msdn.microsoft.com/library/windows/hardware/ff551054)并[ **IInterFilterCommunicator::RequestWriter** ](https://msdn.microsoft.com/library/windows/hardware/ff551057)方法**IInterfilterCommunicator**接口 (pIInterFilterCom) 来初始化筛选器的提供程序和使用者接口。

如果数据包含 PrintTicket 部分，您可以通过 Microsoft Win32 PrintTicket 或 PrintCapabilities API 访问数据。 对于基于 XPSDrv UniDrv 和 PScript5 驱动程序，筛选器可以有权访问[IPrintCoreHelper](https://msdn.microsoft.com/library/windows/hardware/ff552960)接口核心 Unidrv 或 PScript5 驱动程序，因为其配置服务。

筛选器可能还可以通过属性包，具体取决于驱动程序设计访问专有的配置数据。

间的筛选器 Communicator 是一部分的筛选器管道管理器处理筛选器管道中的筛选器之间的通信。 当筛选器管道管理器初始化筛选器，间的筛选器 Communicator 接口 ([IInterFilterCommunicator](https://msdn.microsoft.com/library/windows/hardware/ff551050)) 传递给筛选器，以便筛选器可以获取读取和写入该定义的接口筛选器。

Microsoft 提供的 XPS 文档和流接口，但您可以创建为该筛选器定义您自己间的筛选器接口。 Microsoft 提供了以下接口：

-   XPS 文档界面中读取和写入 XPS 假脱机文件的不同部分。

-   XPS 流接口读取和写入数据的串行流。 您可以使用此接口来编写页面描述语言 (PDL) 从筛选器不使用 XPS 作为 PDL 打印机。

筛选器必须符合的呈现规则和定义 XML 纸张规范 (XPS) 中的 PrintTicket 处理规则。

筛选器必须依赖于 Microsoft.NET 公共语言运行时 (CLR) 或 Microsoft WinFX 运行时组件。

管道中的筛选器不能显示用户界面内容。

以下建议适用于筛选器：

-   筛选器不应创建单独的进程或线程。 如果单独的进程或线程是必需的筛选器必须正确管理进程或线程生存期。

-   筛选器应拥有独立的功能。 所有功能和实现应该都是模块化。 消除筛选器尽可能之间任何顺序和功能的依赖关系。

-   筛选器应处理在其中被放入管道无序的情况。 当筛选器未处于预期的顺序时，它不应崩溃，并应尽可能适当处理这种情况。 如果筛选器依赖于另一个筛选器，它应如果依赖项未提供适当地处理这种情况。

有关将异步通知添加到筛选器的详细信息，请参阅[打印筛选器中的异步通知](asynchronous-notifications-in-print-filters.md)。

 

 





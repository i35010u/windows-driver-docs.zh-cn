---
title: 实现 XPS 筛选器
description: 实现 XPS 筛选器
ms.assetid: 681f533f-d6f6-43a3-be0b-10d8c1a6f12e
keywords:
- XPSDrv 打印机驱动程序 WDK，呈现模块
- 渲染模块 WDK XPSDrv，XPS 筛选器
- XPS 筛选器 WDK XPSDrv
- 筛选 WDK XPS
- IPrintPipelineFilter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d41f4eab5a3942abb6461e5dc65516b6cd05e82a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844839"
---
# <a name="implementing-xps-filters"></a>实现 XPS 筛选器


所有 XPS 筛选器必须实现[IPrintPipelineFilter](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintpipelinefilter)接口。

在调用[**IPrintPipelineFilter：： InitializeFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nf-filterpipeline-iprintpipelinefilter-initializefilter)方法期间，筛选器应：

1.  缓存指向[IPrintPipelineManagerControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintpipelinemanagercontrol)接口的指针。

2.  在[IPrintPipelinePropertyBag](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintpipelinepropertybag)接口中处理相关数据。

3.  调用**IInterFilterCommunicator**接口（pIInterFilterCom）的[**IInterFilterCommunicator：： RequestReader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nf-filterpipeline-iinterfiltercommunicator-requestreader)和[**IInterFilterCommunicator：： RequestWriter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nf-filterpipeline-iinterfiltercommunicator-requestwriter)方法，初始化的提供程序和使用者接口筛选器。

如果数据包含 PrintTicket 部分，则可以通过 Microsoft Win32 PrintTicket 或 PrintCapabilities API 访问数据。 对于基于 XPSDrv 的 UniDrv 和 PScript5 驱动程序，筛选器可以访问[IPrintCoreHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelper) Interface core UniDrv 或 PScript5 driver 作为其配置服务。

筛选器还可以通过属性包访问专用的配置数据，具体取决于驱动程序设计。

筛选器间 Communicator 是筛选器管道管理器的一部分，用于处理筛选器管道中筛选器之间的通信。 当筛选器管道管理器初始化筛选器时，会将一个筛选器 Communicator 接口（[IInterFilterCommunicator](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iinterfiltercommunicator)）传递给该筛选器，以便筛选器可以获取为该筛选器定义的读取和写入接口。

Microsoft 提供 XPS 文档和流接口，但你可以创建自己的筛选器内部筛选器接口。 Microsoft 提供以下接口：

-   XPS 文档界面从 XPS 假脱机文件的不同部分进行读取和写入。

-   XPS 流接口读取并写入序列数据流。 此接口可用于将页面描述语言（PDL）从筛选器写入到不使用 XPS 作为 PDL 的打印机。

筛选器必须符合 XML 纸张规范（XPS）中定义的呈现规则和 PrintTicket 处理规则。

筛选器不能依赖于 Microsoft .NET 公共语言运行时（CLR）或 Microsoft WinFX 运行时组件。

管道中的筛选器不能显示用户界面内容。

以下建议适用于筛选器：

-   筛选器不应创建单独的进程或线程。 如果需要单独的进程或线程，筛选器必须正确地管理进程或线程生存期。

-   筛选器应具有独立功能。 所有功能和实现都应该是模块化的。 尽可能消除筛选器之间的任何订单和功能依赖关系。

-   筛选器应处理在管道中将其放入管道中的情况。 如果筛选器未按预期顺序出现，则它不应崩溃并应适当地处理这种情况。 如果筛选器依赖于其他筛选器，则在未提供依赖项的情况下，它应正常处理此情况。

有关将异步通知添加到筛选器的详细信息，请参阅[打印筛选器中的异步通知](asynchronous-notifications-in-print-filters.md)。

 

 





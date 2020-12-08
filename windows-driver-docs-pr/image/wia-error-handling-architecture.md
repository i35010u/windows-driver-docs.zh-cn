---
title: WIA 错误处理体系结构
description: WIA 错误处理体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18afea89e4ff19a1933b4bcb755b572a1c9e39d3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840365"
---
# <a name="wia-error-handling-architecture"></a>WIA 错误处理体系结构


WIA 错误处理体系结构由三个部分组成。 操作系统、驱动程序和应用程序。 错误处理机制依赖于基于流的数据传输。 此传输模型在 Windows Vista 和更高版本的操作系统中可用。 如果要支持此新的错误处理方法，必须编写 WIA 驱动程序来利用此传输模型。 同样，还必须编写应用程序以支持基于流的传输模型，才能将其部分置于此新的错误处理体系结构中。

WIA 错误处理由系统提供、IHV 提供和 ISV 提供的组件组成。 下图说明了每个组件的供应商。

![说明 wia 错误处理组件的关系图](images/wia-error-wv.png)

有三个可能的错误处理程序：应用程序错误处理程序、驱动程序错误处理程序和默认的错误处理程序。 下面的关系图显示了这三个错误处理程序。

![阐释三个 wia 错误处理程序的关系图](images/wia-errorhandlers.png)

该图像还显示了 WIA 代理回调尝试这三个错误处理程序的层次结构。

大多数情况下，这些处理程序是相同的。 但有几个不同之处。 应用程序错误处理程序实现了 **IWiaAppErrorHandler** 接口，而驱动程序错误处理扩展插件和默认的错误处理程序实现了 **IWiaErrorHandler** 接口。 应用程序错误处理程序还将使用 **IWiaTransferCallback**，它必须在回调对象中实现。

使用 **IWiaErrorHandler：： ReportStatus** 的 *hrStatus* 参数将设备状态代码传递到错误处理程序。 此值与微型驱动程序在 **IWiaTransferCallback：： WiaTransferParams** 方法的 *hrErrorStatus* 参数中设置的值相同。

如果 *hrStatus* 参数设置为 \_ "成功"，则它表示非致命延迟。 这意味着错误处理 UI 只应提供无模式的信息性对话框，并有机会取消传输。 每当错误处理程序收到具有不同 *hrStatus* 值的消息时，UI 应关闭， (错误处理程序是否支持此消息) 。

**注意**   同时只能显示一个无模式错误处理程序对话框。

 

错误处理程序应显示模式用户界面，以响应严重错误的设备状态消息 \_ 。

WIA 错误处理涉及四个组件：

<a href="" id="the-wia-minidriver"></a>**WIA 微型驱动程序**  
现在，微型驱动程序可以使用，Windows Vista 的新增功能，WIA \_ 传输 \_ 消息 \_ 设备状态 \_ 设备状态消息指示设备级别发生了某些事情。 当驱动程序发送此消息时，它还必须设置 *hrErrorStatus* (，并可能同时设置 **IWiaTransferCallback：： WiaTransferParams** 方法的 *lPercentComplete*) 参数。 状态代码可以是错误或信息。 如果出现错误状态代码，则需要用户干预才能从错误中恢复，从而能够恢复错误。 驱动程序可以将 *hrErrorStatus* 设置为预定义的 wia HRESULT 值，例如 wia \_ 状态 \_ 预热 \_ ，或创建自己的自定义 HRESULT。

<a href="" id="the-application-error-handler"></a>**应用程序错误处理程序**  
为了使应用程序能够启用错误处理，它必须实现 **IWiaAppErrorHandler** 接口。 此接口由应用程序的回调对象实现，该对象将其传递到 **IWiaTransfer：:D o)** 和 **IWiaTransfer：：上传** 方法。 此回调对象是实现 **IWiaTransferCallback** 接口所必需的。 通过实现 **IWiaAppErrorHandler**，应用程序表示它允许在数据传输过程中调用错误处理程序。

<a href="" id="the-driver-s-error-handler"></a>**驱动程序的错误处理程序**  
驱动程序的错误处理程序是必须实现 [IWiaErrorHandler 接口](/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiaerrorhandler)的驱动程序扩展。 错误处理程序可以处理和显示任何状态代码的 UI;这些状态代码包括 WIA 定义的状态代码，以及特定于该驱动程序的状态代码。

<a href="" id="the-default-error-handler"></a>**默认错误处理程序**  
默认错误处理程序由 WIA 实现。 它处理并显示许多通用设备状态消息的 UI。 这些消息可以是信息性消息和错误消息，例如： WIA \_ 错误 \_ 卡纸 \_ 和 wia \_ 状态 \_ 预热 \_ 。

WIA 代理不处理错误消息本身。 相反，WIA 代理使错误处理程序有机会处理设备状态消息。

错误处理程序提供用户界面，使用户可以尝试将系统置于可以继续或取消数据传输的状态。

接收 WIA \_ 传输 \_ 消息 \_ 设备 \_ 状态消息时，wia 代理首先调用应用程序错误处理程序的 **IWiaAppErrorHandler：： ReportStatus** 方法。 如果应用程序回调例程不处理设备状态代码，WIA 代理将调用驱动程序错误处理程序的 [**IWiaErrorHandler：： ReportStatus**](/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiaerrorhandler-reportstatus) 实现，最后，wia 代理将调用默认错误处理程序的 **IWiaErrorHandler：： ReportStatus** 实现。 如果给定的处理程序不存在 (例如，驱动程序可能不附带错误处理扩展插件) ，或者，如果驱动程序的设备状态处理程序返回 \_ 未处理的 WIA 状态 \_ \_ ，表明驱动程序的处理程序不支持设备代码，则会向链中的下一个处理程序提供机会。 一旦成功或未成功处理设备状态消息，WIA 代理回调就会返回。 因此，如果驱动程序错误处理程序的 **ReportStatus** 方法 \_ 为每条消息返回 s OK，则默认错误处理程序将永远不会有机会处理任何设备状态消息。

如果没有错误处理程序支持带有严重性错误的设备状态消息 \_ (错误消息) ，WIA 代理会将状态错误返回给驱动程序，进而停止传输。 驱动程序应从 IWiaMiniDrv 中返回此 HRESULT 值 [**：:D rvacquireitemdata**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata) ，应用程序将从 **IWiaTransfer：:D o)** 或 **IWiaTransfer：：上载** 接收此 hresult。

如果没有错误处理程序处理严重成功的设备状态消息 \_ (信息性消息) ，WIA 代理会 \_ 向驱动程序返回 "OK"。

**注意**  应用程序的回调例程 **IWiaTransferCallback：： TransferCallback** 永远不会收到一条消息，其中 *LMESSAGE* 设置为 WIA \_ 传输 \_ 消息 \_ 设备 \_ 状态。 相反，这些消息将发送到错误处理程序。

 

Microsoft Windows SDK 文档中介绍了 **IWiaTransferCallback**、**IWiaAppErrorHandler** 和 **IWiaTransfer** 接口。

 


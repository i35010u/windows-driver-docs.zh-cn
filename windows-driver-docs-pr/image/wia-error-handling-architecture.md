---
title: WIA 错误处理体系结构
description: WIA 错误处理体系结构
ms.assetid: 2672a5ee-d860-44de-9e68-bd70377d58a8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 013671a2d138417f0c495a4607a6018a94241348
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355783"
---
# <a name="wia-error-handling-architecture"></a>WIA 错误处理体系结构


WIA 错误处理体系结构由以下三个部分组成。 操作系统、 驱动程序和应用程序。 错误处理机制依赖于基于流的数据传输。 此传输模型是在 Windows Vista 和更高版本操作系统中可用。 必须编写 WIA 驱动程序以便使用此传输模型，若要支持此新的错误处理方法。 同样，应用程序，还必须编写为支持基于流传输模式能够参与其此新的错误处理体系结构。

WIA 错误处理由系统提供、 提供 IHV 和 ISV 提供的组件构成。 下图说明了每个组件的供应商。

![说明 wia 错误处理组件的关系图](images/wia-error-wv.png)

有三个可能的错误处理程序： 应用程序错误处理程序、 驱动程序错误处理程序，并默认错误处理程序。 下图中显示这些三个错误处理程序。

![说明三个 wia 错误处理程序的关系图](images/wia-errorhandlers.png)

下图还显示由 WIA 代理回调尝试这些三个错误处理程序时的层次结构。

在大多数方面，这些处理程序是相同的。 有一些但是的差异。 应用程序错误处理程序实现**IWiaAppErrorHandler**而驱动程序错误处理扩展插件和默认错误处理程序实现的接口**IWiaErrorHandler**接口。 应用程序错误处理程序还将使用**IWiaTransferCallback**，其必须实现的回调对象中。

设备状态代码传递到的错误处理程序与*hrStatus*的参数**IWiaErrorHandler::ReportStatus**。 这是微型驱动程序设置中的相同值*hrErrorStatus*的参数**IWiaTransferCallback::WiaTransferParams**方法。

如果*hrStatus*参数设置为严重性\_成功后，它表示非严重延迟。 这意味着无模式、 信息性对话框，并可以选择取消此转移应只是提供错误处理 UI。 UI 应该消除错误处理程序收到的消息具有不同的下次*hrStatus* （是否错误处理程序支持此消息） 的值。

**请注意**  只有一个无模式的错误处理程序对话框可以显示在同一时间。

 

错误处理程序应在响应的严重性的设备状态消息中显示模式 UI\_错误。

有四个组件参与 WIA 错误处理：

<a href="" id="the-wia-minidriver"></a>**WIA 微型驱动程序**  
微型驱动程序现在可以使用，new Windows vista，WIA\_传输\_MSG\_设备\_状态设备的状态消息，指示内容发生在设备级别。 当驱动程序发送此消息时，它还必须设置*hrErrorStatus* (以及可能还*lPercentComplete*) 的参数**IWiaTransferCallback::WiaTransferParams**方法。 状态代码可以是一个错误消息或信息性。 如果错误状态代码，需要用户干预从提供的错误可恢复的错误中恢复。 驱动程序可以设置*hrErrorStatus*为预定义的 WIA HRESULT 值，例如 WIA\_状态\_WARMING\_最多，或创建其自己自定义的 HRESULT。

<a href="" id="the-application-error-handler"></a>**应用程序错误处理程序**  
为了使应用程序以启用错误处理，它必须实现**IWiaAppErrorHandler**接口。 此接口由它传递到的应用程序的回调对象实现**IWiaTransfer::Download**并**IWiaTransfer::Upload**方法。 此回调对象必须实现**IWiaTransferCallback**接口。 通过实现**IWiaAppErrorHandler**，应用程序指示它允许在数据传输过程中调用错误处理程序。

<a href="" id="the-driver-s-error-handler"></a>**驱动程序的错误处理程序**  
驱动程序的错误处理程序是一个驱动程序扩展，必须实现[IWiaErrorHandler 接口](https://msdn.microsoft.com/library/windows/hardware/ff543907)。 错误处理程序可以处理和显示 UI 的任何状态代码;这些状态代码包括 WIA 定义状态代码和特定于驱动程序的状态代码。

<a href="" id="the-default-error-handler"></a>**默认错误处理程序**  
由 WIA 实现默认错误处理程序。 它处理，并显示 UI 的通用设备状态消息数。 这些消息可以是这两条信息性和错误，例如：WIA\_错误\_纸张\_卡纸问题和 WIA\_状态\_WARMING\_向上。

WIA 代理不处理的错误消息本身。 相反，WIA 代理提供错误处理程序处理设备的状态消息的机会。

错误处理程序提供 UI，可让用户以尝试使系统处于可以继续或取消数据传输的状态。

当接收 WIA\_传输\_MSG\_设备\_状态消息，WIA 代理首先调用应用程序错误处理程序的**IWiaAppErrorHandler::ReportStatus**方法。 如果应用程序回调例程不会处理设备状态代码，WIA 代理将调用驱动程序错误处理程序的[ **IWiaErrorHandler::ReportStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff543909)实现，并最后 WIA代理将调用默认错误处理程序的**IWiaErrorHandler::ReportStatus**实现。 如果不存在给定的处理程序 （例如，驱动程序可能不提供有一个错误处理扩展插件），或如果驱动程序的设备状态处理程序返回 WIA\_状态\_不\_已处理，指示驱动程序的处理程序不支持设备代码中，链中的下一个处理程序将提供了机会。 处理设备的状态消息、 成功或失败，将返回 WIA 代理回调。 因此，如果驱动程序错误处理程序的**ReportStatus**方法将返回 S\_确定对每个消息默认错误处理程序将永远不会有机会处理任何设备的状态消息。

没有错误处理程序是否支持设备状态消息严重性\_错误 （错误消息），WIA 代理将返回状态错误，返回到驱动程序，进而应停止传输。 该驱动程序应返回此 HRESULT 值从[ **IWiaMiniDrv::drvAcquireItemData** ](https://msdn.microsoft.com/library/windows/hardware/ff543956)并且该应用程序将收到来自此 HRESULT **IWiaTransfer::Download**或**IWiaTransfer::Upload**。

如果将没有错误处理程序处理设备的状态消息严重性\_WIA 代理将返回成功 （信息性消息），S\_向驱动程序的确定。

**请注意**  应用程序的回调例程**IWiaTransferCallback::TransferCallback**，将永远不会收到一条消息与*lMessage*设置为 WIA\_传输\_MSG\_设备\_状态。 相反，这些消息将发送到错误处理程序。

 

**IWiaTransferCallback**，**IWiaAppErrorHandler**，并**IWiaTransfer**接口 Microsoft Windows SDK 文档中所述。

 

 





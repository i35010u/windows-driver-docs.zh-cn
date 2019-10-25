---
title: 在旧版应用程序和 Windows Vista 驱动程序之间进行的数据传输
description: 在旧版应用程序和 Windows Vista 驱动程序之间进行的数据传输
ms.assetid: 83817277-3526-4f64-8e7c-7e02c8cd77bd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05f67fd84e93d8c7662adf7c2ce69c59dc2b4c6a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840860"
---
# <a name="data-transfer-between-legacy-application-and-windows-vista-driver"></a>在旧版应用程序和 Windows Vista 驱动程序之间进行的数据传输


兼容层必须确保始终调用驱动程序的图像处理筛选器，并且不显式支持**LocalService**帐户的旧应用程序仍将能够执行数据传输。 **LocalService**帐户在 MICROSOFT Windows XP 和更高版本的操作系统上可用。

旧驱动程序必须至少同时公开 TYMED\_文件和 TYMED\_回调;但是，Windows Vista 驱动程序永远不会公开 TYMED\_回调（或 TYMED\_多页\_回调）。 兼容性层的传输部分将确保旧版应用程序在 Windows Vista 驱动程序未实现的情况 TYMED\_回叫。 TYMED\_多页\_回调永远不会从 Windows Vista 驱动程序公开。

旧版应用程序将显示 Windows Vista 驱动程序公开的 TYMED\_文件和 TYMED\_多页\_文件所支持的格式。 对于 TYMED\_回调，旧应用程序将看到与驱动程序为 TYMED\_文件公开的格式相同的格式，但有一个例外：而不是公开**WiaImgFmt\_BMP**，则兼容层将公开**WiaImgFmt\_MEMORYBMP**到旧版应用程序。 完成此操作的方法是将对 IWiaMiniDrv 的调用设置为 "截取" [ **：:D rvgetwiaformatinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo)，并添加所有 Windows Vista 驱动程序的 TYMED\_文件格式（ **WiaImgFmt\_BMP** /**WiaImgFmt\_MEMORYBMP**）对于 TYMED\_回调。 最重要的是，在数据传输过程中，兼容层会创建自己的旧式回调对象，这会将 Windows Vista 传输消息和写入到流中的数据转换为旧传输消息。

有关 TYMED 常量的详细信息，请参阅[了解 TYMED](understanding-tymed.md)。

兼容性层在 WIA COM 代理中创建两个回调对象：一个用于回调传输，另一个用于文件传输。 WIA COM 代理实现了[IWiaTransferCallback 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiatransfercallback)。 此回调对象负责在基于流的传输和 "旧样式" 传输之间进行转换。 WIA 兼容性层还会启动驱动程序的图像处理筛选器，通过兼容层的回调对象。 因此，图像处理筛选器将始终在应用程序的上下文中运行，就像在 Windows Vista 传输过程中一样。

下图说明了兼容层如何适用于 Windows Vista 驱动程序和旧版应用程序。

![说明旧应用程序和 windows vista 驱动程序之间的数据传输的关系图](images/vistaapp-legacydrv.png)

WIA COM 代理中的旧回调对象将 Windows Vista 传输消息和写入到流中的数据转换为旧传输消息，并将数据写入文件或联合数据回调。

当驱动程序调用由它从[**IWiaMiniDrvTransferCallback：： GetNextStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvtransfercallback-getnextstream)方法接收的**IStream**接口公开的任何方法时（请注意，驱动程序应仅调用**IStream：： Write**、 **IStream：： Seek**和**IStream：： SetSize**）。 因此，兼容层创建了一个自定义的**IStream**实现，该实现只包装 WIA COM 代理提供的**istream**接口。

旧式文件传输非常简单。 例如，当旧应用程序调用**IWiaDataTransfer：： idtGetData**时，就会出现这种传输。 兼容性层在应用程序在 STGMEDIUM 结构中指定的文件上创建数据流。 此流将在调用[**IWiaTransferCallback：： GetNextStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiatransfercallback-getnextstream)时传递到驱动程序或图像处理筛选器，并且所有传输消息都可以轻松地映射到旧式传输消息。 有关如何映射消息的更详细说明，请参阅[WIA 兼容层数据传输实现](wia-compatibility-layer-message-mapping.md)。

调用**IWiaDataTransfer：:D tgetdata 方法**时，兼容层执行一些更严格的参数检查。 例如，兼容性层不允许使用[TYMED\_文件](understanding-tymed.md)调用**IWiaDataTrasnfer：： idtGetData**方法，在不利用兼容性层的数据传输中，一个页面计数可以调用带有 TYMED\_文件的**IWiaDataTrasnfer：： idtGetData**方法，并将页计数增加一。

旧的回调传输有点棘手。 由于 Windows Vista 驱动程序不支持**WiaImgFmt\_MEMORYBMP**（这是旧驱动程序所必需的），因此兼容层的回调对象必须处理从**WiaImgFmt\_BMP**到**WiaImgFmt 的转换\_MEMORYBMP**。 传输消息之间的映射也不是非常简单。 兼容层创建其自己的流实现。 当应用程序调用**IStream：： Write**方法时，兼容层向应用程序的回调发送\_消息\_数据消息。

在实现兼容性层的过程中，必须对**IWiaTransfer**接口进行更改;将函数**IWiaTransfer：： EnumWIA\_\_格式**添加到**IWiaTransfer** ，以允许 TYMED\_多页\_文件传输。 此添加不是兼容性层的结果，但这是必需的，因为无法从**IWiaTransfer**接口或从**IWiaItem2**接口到**IWiaItem**的**IWiaDataTransfer**接口交互.

Microsoft Windows SDK 文档中讨论了**IWiaDataTransfer**、 **IWiaTransfer**、 **IWiaItem**、 **IWiaItem2**和**IStream**接口以及 STGMEDIUM 结构。

## <a name="related-topics"></a>相关主题
[**IWiaMiniDrvTransferCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvtransfercallback)  




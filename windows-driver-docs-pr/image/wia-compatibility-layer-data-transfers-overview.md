---
title: WIA 兼容性层数据传输概述
description: WIA 兼容性层数据传输概述
ms.assetid: 4c88474e-f776-4876-a15f-c9d6fb0d20e5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72dd82a8b3253e6ccd432aa83c348a7abb0a67eb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840723"
---
# <a name="wia-compatibility-layer-data-transfers-overview"></a>WIA 兼容性层数据传输概述


如果没有传输兼容性层，Windows Vista WIA 驱动程序必须实现 TYMED 和基于流的数据传输样式，才能执行从旧版本和 Windows Vista 应用程序进行的数据传输。 同样，Windows Vista WIA 应用程序必须实现两种传输样式（具有不同的回调实现），以便能够从旧版本和 Windows Vista 驱动程序执行数据传输。 使用 WIA 兼容层，驱动程序类型对 WIA 应用程序而言是透明的，而 Windows Vista WIA 驱动程序则不必处理任何旧式传输代码。

在两种传输案例中，需要一个兼容层，其中每个都可以进一步细分为两个子类别：

1.  从 Windows Vista 驱动程序传输数据的旧应用程序：
    1.  文件传输：应用程序调用**IWiaDataTransfer：： idtGetBandedData**。
    2.  回调传输：应用程序调用**IWiaDataTransfer：： idtGetData**。

2.  从旧驱动程序传输数据的 Windows Vista 应用程序：
    1.  文件传输：兼容层启动带有旧驱动程序的文件传输。
    2.  回拨传输：兼容层启动与旧驱动程序的回调传输。

确定是否使用兼容性层的第一步是确定 WIA 驱动程序是 Windows Vista 驱动程序还是旧驱动程序。 WIA 服务将通过查看驱动程序从[**IStiUSD：： GetCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getcapabilities)返回的版本号来确定这一点。 旧驱动程序返回版本号的 STI\_版本，而 Windows Vista 驱动程序必须返回\_STI 版本\_3。 此版本号将公开给 Windows Vista 属性中的 WIA COM 代理（和 WIA 应用程序），WIA\_DIP\_STI\_DRIVER\_版本。

确定是否使用兼容性层的下一步是确定应用程序是否为 Windows Vista WIA 应用程序或旧版 WIA 应用程序是否很简单：如果应用程序调用**IWiaDataTransfer：： idtGetBandedData**或**IWiaDataTransfer：： idtGetData**它是一个旧版 WIA 应用程序，如果应用程序调用**IWiaTransfer：:D o)** 它是一个 Windows Vista WIA 应用程序。

对于基于流的新数据传输模型，WIA 服务将不再区分 TYMED\_回调和 TYMED\_文件（或 TYMED\_多页\_回调和 TYMED\_文件）。 而只有 TYMED\_文件和 TYMED\_多页\_文件中。 需要 TYMED\_多页面\_文件，才能允许驱动程序支持多页 TIFF （或 PDF）扫描。 有关 TYMED 常量的详细信息，请参阅[了解 TYMED](understanding-tymed.md)。

WIA 在 Windows Vista 驱动程序中不支持**WiaImgFmt\_MEMORYBMP**的内存位图格式。

Windows Vista 驱动程序可以发送更新消息以在带区传输数据，而不是在传输过程中让驱动程序缓存整个映像。 这种形式的传输可用于在扫描过程中传输数据，在这种情况下，不能立即确定要传输的图像的大小，例如，使用滚动源扫描程序进行扫描。 为了传输带区中的图像数据，驱动程序必须在[**IWiaTransferCallback：： GetNextStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiatransfercallback-getnextstream)中传递给它的流上调用**IStream：： Seek** 。

有关 TYMED 和基于流的传输的其他信息，请参阅[数据传输](data-transfers.md)。

Microsoft Windows SDK 文档中讨论了**IWiaDataTransfer**、 **IWiaTransfer**和**IStream**接口。

 

 





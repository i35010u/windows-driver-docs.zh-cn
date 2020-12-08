---
title: WIA 兼容性层数据传输概述
description: WIA 兼容性层数据传输概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33a361ebaa34c08413aa52779af83df4e509b09a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831797"
---
# <a name="wia-compatibility-layer-data-transfers-overview"></a>WIA 兼容性层数据传输概述


如果没有传输兼容性层，Windows Vista WIA 驱动程序必须实现 TYMED 和基于流的数据传输样式，才能执行从旧版本和 Windows Vista 应用程序进行的数据传输。 同样，Windows Vista WIA 应用程序必须实现 (具有不同回调实现的传输的两种样式，) 才能执行来自旧版本和 Windows Vista 驱动程序的数据传输。 使用 WIA 兼容层，驱动程序类型对 WIA 应用程序而言是透明的，而 Windows Vista WIA 驱动程序则不必处理任何旧式传输代码。

在两种传输案例中，需要一个兼容层，其中每个都可以进一步细分为两个子类别：

1.  从 Windows Vista 驱动程序传输数据的旧应用程序：
    1.  文件传输：应用程序调用 **IWiaDataTransfer：： idtGetBandedData**。
    2.  回调传输：应用程序调用 **IWiaDataTransfer：： idtGetData**。

2.  从旧驱动程序传输数据的 Windows Vista 应用程序：
    1.  文件传输：兼容层启动带有旧驱动程序的文件传输。
    2.  回拨传输：兼容层启动与旧驱动程序的回调传输。

确定是否使用兼容性层的第一步是确定 WIA 驱动程序是 Windows Vista 驱动程序还是旧驱动程序。 WIA 服务将通过查看驱动程序从 [**IStiUSD：： GetCapabilities**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getcapabilities)返回的版本号来确定这一点。 旧驱动程序返回 \_ 版本号的 STI 版本，而 Windows Vista 驱动程序必须返回 STI \_ 版本 \_ 3。 此版本号将公开给 WIA COM proxy (和 WIA 应用程序) 在 Windows Vista 属性，WIA \_ DIP \_ STI \_ 驱动程序 \_ 版本中。

确定是否使用兼容性层的下一步是确定应用程序是否为 Windows Vista WIA 应用程序或旧的 WIA 应用程序是否很简单：如果应用程序调用 **IWiaDataTransfer：： idtGetBandedData** 或 **IWiaDataTransfer：： idtGetData** ，则它是旧版 WIA 应用程序，如果应用程序调用 **IWiaTransfer：:D O)** 它是 Windows Vista WIA 应用程序。

对于基于流的新数据传输模型，WIA 服务将不再区分 TYMED \_ 回调和 TYMED \_ 文件 (或 TYMED \_ 多页 \_ 回调和 TYMED \_ 多页 \_ 文件) 。 相反，将只有 TYMED \_ 文件和 TYMED \_ 多页 \_ 文件。 \_需要 TYMED 多 \_ 页文件，才能允许驱动程序支持多页 TIFF (或 PDF) 扫描。 有关 TYMED 常量的详细信息，请参阅 [了解 TYMED](understanding-tymed.md)。

WIA 将不支持 Windows Vista 驱动程序中的内存位图格式 **WiaImgFmt \_ MEMORYBMP** 。

Windows Vista 驱动程序可以发送更新消息以在带区传输数据，而不是在传输过程中让驱动程序缓存整个映像。 这种形式的传输可用于在扫描过程中传输数据，在这种情况下，不能立即确定要传输的图像的大小，例如，使用滚动源扫描程序进行扫描。 为了传输带区中的图像数据，驱动程序必须在 [**IWiaTransferCallback：： GetNextStream**](/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiatransfercallback-getnextstream)中传递给它的流上调用 **IStream：： Seek** 。

有关 TYMED 和基于流的传输的其他信息，请参阅 [数据传输](data-transfers.md)。

Microsoft Windows SDK 文档中讨论了 **IWiaDataTransfer**、 **IWiaTransfer** 和 **IStream** 接口。

 


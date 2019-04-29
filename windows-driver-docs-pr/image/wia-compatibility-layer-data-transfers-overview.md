---
title: WIA 兼容性层数据传输概述
description: WIA 兼容性层数据传输概述
ms.assetid: 4c88474e-f776-4876-a15f-c9d6fb0d20e5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14df38f512094aad337741984f3d3cf093b3023f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360619"
---
# <a name="wia-compatibility-layer-data-transfers-overview"></a>WIA 兼容性层数据传输概述


而无需传输兼容性层，Windows Vista WIA 驱动程序将不得不若要从旧版查询语言和 Windows Vista 应用程序执行数据传输将实现 TYMED 和基于流的数据传输样式。 同样，Windows Vista WIA 应用程序将不得不若要从旧版查询语言和 Windows Vista 驱动程序执行数据传输将实现 （与不同的回调实现） 的传输这两种样式。 使用 WIA 兼容性层，驱动程序的类型是透明的 WIA 应用程序和 Windows Vista WIA 驱动程序不需要任何旧传输代码处理。

有两种传输情况下需要一个兼容性层的位置，其中每个可以进一步分解为两个子类别：

1.  从 Windows Vista 驱动程序传输数据的旧应用程序：
    1.  文件传输：应用程序调用**IWiaDataTransfer::idtGetBandedData**。
    2.  回调传输：应用程序调用**IWiaDataTransfer::idtGetData**。

2.  将数据从旧驱动程序传输到 Windows Vista 应用程序：
    1.  文件传输：兼容性层启动文件传输使用旧驱动程序。
    2.  回调传输：兼容性层启动回调传输与旧驱动程序。

确定是否使用兼容性层确定是否 WIA 驱动程序是 Windows Vista 驱动程序或旧版的驱动程序中的第一个步骤。 WIA 服务将通过查看在驱动程序从返回的版本编号来确定这[ **IStiUSD::GetCapabilities**](https://msdn.microsoft.com/library/windows/hardware/ff543817)。 旧驱动程序返回 STI\_版本的版本编号，而 Windows Vista 驱动程序必须返回 STI\_版本\_3。 此版本号会公开给 WIA COM 代理 （和 WIA 应用程序） 在 Windows Vista 属性中，WIA\_DIP\_STI\_驱动程序\_版本。

确定是否使用兼容性层的下一步是确定应用程序是 Windows Vista WIA 应用程序还是旧 WIA 应用程序很简单： 在应用程序调用**IWiaDataTransfer::idtGetBandedData**或**IWiaDataTransfer::idtGetData**它是旧的 WIA 应用程序，如果应用程序调用**IWiaTransfer::Download**它是 Windows Vista WIA 应用程序。

新的基于流的数据传输模型，WIA 服务将无法再区分 TYMED\_回调和 TYMED\_文件 (或 TYMED\_多页\_回调和 TYMED\_多页\_文件）。 而是仅有 TYMED\_文件和 TYMED\_多页\_文件。 TYMED\_多页\_允许驱动程序以支持多页 TIFF （或 PDF） 扫描所需的文件。 有关 TYMED 的详细信息请参阅常量[了解 TYMED](understanding-tymed.md)。

内存位图格式不支持 WIA **WiaImgFmt\_MEMORYBMP** Windows Vista 驱动程序中。

Windows Vista 驱动程序可以发送更新消息，而不会让驱动程序在传输过程缓存整个图像将带区中的数据。 这种形式的传输可用于将数据传输在扫描期间，不能立即确定图像传输时，例如，与滚动源扫描程序扫描的大小。 若要将带区中的图像数据传输，该驱动程序必须调用**IStream::Seek**中传递给它的流[ **IWiaTransferCallback::GetNextStream**](https://msdn.microsoft.com/library/windows/hardware/ff545039)。

TYMED 和基于流的传输的其他信息，请参阅[数据传输](data-transfers.md)。

**IWiaDataTransfer**， **IWiaTransfer**，并**IStream** Microsoft Windows SDK 文档中讨论了接口。

 

 





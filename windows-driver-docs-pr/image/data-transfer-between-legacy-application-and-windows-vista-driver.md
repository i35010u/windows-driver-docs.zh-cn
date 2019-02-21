---
title: 旧版应用程序和 Windows Vista 驱动程序之间传输数据
description: 旧版应用程序和 Windows Vista 驱动程序之间传输数据
ms.assetid: 83817277-3526-4f64-8e7c-7e02c8cd77bd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1bafeee84f848d10500ce24baab0b6bf8f52009
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554225"
---
# <a name="data-transfer-between-legacy-application-and-windows-vista-driver"></a>旧版应用程序和 Windows Vista 驱动程序之间传输数据


兼容性层必须确保，将始终调用驱动程序的图像处理筛选器，并且旧的应用程序，不显式支持**LocalService**帐户仍将能够执行数据传输。 **LocalService**帐户，可在 Microsoft Windows XP 和更高版本操作系统上。

旧驱动程序必须至少公开两个 TYMED\_文件和 TYMED\_回调; 但是，Windows Vista 驱动程序将永远不会公开 TYMED\_回调 (或 TYMED\_多页\_回调)。 兼容性层的传输部分将确保旧版应用程序，将看到 TYMED\_回调尽管 Windows Vista 驱动程序不实现它。 TYMED\_多页\_回调将永远不会公开来自 Windows Vista 驱动程序。

旧应用程序将看到 TYMED 支持的格式\_文件和 TYMED\_多页\_Windows Vista 驱动程序公开的文件。 为 TYMED\_回调，旧的应用程序将看到相同的格式如驱动程序公开用于 TYMED\_文件中的，有一个例外： 而不是公开**WiaImgFmt\_BMP**，兼容性层将公开**WiaImgFmt\_MEMORYBMP**到旧应用程序。 工作的方式，即通过兼容性层"截距"对[ **IWiaMiniDrv::drvGetWiaFormatInfo**](https://msdn.microsoft.com/library/windows/hardware/ff543986)，并添加所有 Windows Vista 驱动程序的 TYMED\_文件格式 (与为异常**WiaImgFmt\_BMP** /**WiaImgFmt\_MEMORYBMP**) 的 TYMED\_回调。 最重要的是兼容性层创建其自己旧回调对象在数据传输过程中将 Windows Vista 传输消息和数据写入到其流式传输到旧传输消息的转换。

有关 TYMED 常量的详细信息，请参阅[了解 TYMED](understanding-tymed.md)。

兼容性层 WIA COM 代理中创建两个回调对象： 一个用于回调传输和一个用于文件传输。 WIA COM 代理实现[IWiaTransferCallback 接口](https://msdn.microsoft.com/library/windows/hardware/ff545043)。 此回调对象负责基于流的传输和"老式"传输之间的转换。 WIA 兼容性层还会启动驱动程序的图像处理筛选器，我们将向其传递兼容性层的回调对象。 因此，图像处理筛选器将始终运行应用程序的上下文中就像使用 Windows Vista 传输。

下图演示了使用 Windows Vista 驱动程序和旧的应用程序兼容性层工作原理。

![说明数据传输的旧版应用程序和 windows vista 驱动程序之间的关系图](images/vistaapp-legacydrv.png)

WIA COM 代理中的旧回调对象将 Windows Vista 传输消息和数据写入到流式传输到旧传输消息，并将数据写入到文件或联合的数据回调。

当驱动程序调用的任何公开的方法**IStream**接口，它接收来自[ **IWiaMiniDrvTransferCallback::GetNextStream** ](https://msdn.microsoft.com/library/windows/hardware/jj151551)方法 (请注意驱动程序只应调用**IStream::Write**， **IStream::Seek**，并**IStream::SetSize**)。 因此，兼容性层创建一个自定义**IStream**实现，它只是包装**IStream** WIA COM 代理提供的接口。

旧的文件传输都是非常简单。 此类传输的一个示例是当旧应用程序调用**IWiaDataTransfer::idtGetData**。 兼容性层应用程序指定 STGMEDIUM 结构中的文件上创建的数据流。 调用时，此流被传递给驱动程序或图像处理筛选器[ **IWiaTransferCallback::GetNextStream** ](https://msdn.microsoft.com/library/windows/hardware/ff545039)和传输的所有消息轻松地都映射到旧传输消息。 有关如何将消息映射的更详细说明，请参阅[WIA 兼容性层数据传输实现](wia-compatibility-layer-message-mapping.md)。

调用时**IWiaDataTransfer::dtGetData 方法**，兼容性层会执行一些更严格的参数检查。 例如，兼容性层不允许调用**IWiaDataTrasnfer::idtGetData**方法替换[TYMED\_文件](understanding-tymed.md)和更高版本中的数据传输，则页计数不这样做利用，就可以调用的兼容性层**IWiaDataTrasnfer::idtGetData**方法替换 TYMED\_文件计数更大的页面，然后之一。

旧回调传输都是有点棘手。 因为 Windows Vista 驱动程序不支持**WiaImgFmt\_MEMORYBMP**，这是旧驱动程序的要求，兼容性层的回调对象必须处理从转换**WiaImgFmt\_BMP**到**WiaImgFmt\_MEMORYBMP**。 传输消息之间的映射还不是非常简单。 兼容性层创建其自己的流实现。 兼容性层发送 IT\_MSG\_数据消息时调用的应用程序的回调**IStream::Write**由应用程序的方法。

更改必须对**IWiaTransfer**接口的实现兼容性层; 一部分该函数**IWiaTransfer::EnumWIA\_格式\_信息**添加到**IWiaTransfer**允许 TYMED\_多页\_文件传输。 此添加不是由造成的兼容性层，但需要进行，因为不能访问**IWiaDataTransfer**从接口**IWiaTransfer**接口或从**IWiaItem2**接口**IWiaItem**接口。

**IWiaDataTransfer**， **IWiaTransfer**， **IWiaItem**， **IWiaItem2**，并**IStream**Microsoft Windows SDK 文档中讨论了接口和 STGMEDIUM 结构。

## <a name="related-topics"></a>相关主题
[**IWiaMiniDrvTransferCallback**](https://msdn.microsoft.com/library/windows/hardware/jj151550)  




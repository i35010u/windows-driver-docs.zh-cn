---
title: 在 Windows Vista 应用程序和旧版驱动程序之间进行的数据传输
description: 在 Windows Vista 应用程序和旧版驱动程序之间进行的数据传输
ms.assetid: 0acb2ca3-6ac6-441d-a12d-446ae5b70295
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75ea897f1a5be214671057a2fbdb26fe1db4e132
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364631"
---
# <a name="data-transfer-between-windows-vista-application-and-legacy-driver"></a>在 Windows Vista 应用程序和旧版驱动程序之间进行的数据传输


兼容性层，使 Windows Vista 应用程序可以调用**IWiaTransfer::Download** （Microsoft Windows SDK 文档中所述） 上旧版的驱动程序。 兼容性层必须实现文件夹传输代码，以及格式转换。 兼容性层实现特殊的送纸器传输以确保它始终是最有可能从旧驱动程序转换多个页面的代码。 Windows Vista 应用程序应始终能够从甚至具有 TYMED 的送纸器项在扫描过程中请求多个页\_文件传输。 下图说明了与 Windows Vista 应用程序的旧驱动程序。

![说明 windows vista 应用程序和旧驱动程序之间的数据传输的关系图](images/vistaapp-legacydrv.png)

WIA 服务中的旧回调对象旧传输消息和数据将转换为 Windows Vista 传输消息，并将数据写入到提供的流。

Windows Vista 应用程序仅需要 TYMED\_文件和 TYMED\_多页\_文件，这样的兼容性层负责确保该 TYMED\_回调和 TYMED\_多页\_回调不公开到 Windows Vista 应用程序从旧驱动程序。

实现兼容性层的此部分的最简单方法是始终调用该旧驱动程序带有 TYMED\_文件和 TYMED\_多页\_文件集。 执行此操作的缺点是，该驱动程序将始终不得不扫描整个图像之前的数据无法写回到应用程序的流。 因此，兼容性层使用 TYMED\_回调时 Windows Vista 应用程序请求的格式扫描**WiaImgFmt\_BMP** ( [ **WIA\_IPA\_格式**](https://msdn.microsoft.com/library/windows/hardware/ff551553)属性设置为**WiaImgFmt\_BMP)**。 这使编写数据返回外通过带外的兼容性层。

但是，旧驱动程序不支持**WiaImgFmt\_BMP**，但**WiaImgFmt\_MEMORYBMP**为 TYMED\_回调。 因此，转换回调对象必须创建 BMP 文件标头并重新写入此文件标头也在应用程序。 有时这很容易，如当 BMP 文件标头可以直接从构建 BMP 信息标头。 某些情况下但是 BMP 信息标头的高度设置为 0。 在这种情况下，WIA 兼容性层必须等待，直到所有数据已都传输后，它才能编写 BMP 文件标头并更新 BMP 信息标头。

原因 TYMED 传输时，只需 TYMED 以外\_回调，但是从旧驱动程序是多页的格式通常仅支持通过 TYMED\_多页\_文件和驱动程序通常支持的详细信息格式为 TYMED\_TYMED 的文件比\_回调...

期间 TYMED\_文件传输的兼容性层等待，直到传输完成之前它将数据写回应用程序的流。 这是通过将文件映射到内存并编写在单个回内存中的所有数据都写入请求。

期间 TYMED\_回调传输兼容性层将写回应用程序的流每次收到 IT\_MSG\_旧驱动程序中的数据传输消息。

兼容性层还包含一个特殊的代码的送纸器传输。 此代码可确保，兼容性层可以传输多个页面从 ADF 即使 TYMED 不 TYMED\_多页\_文件。 这是的方法是通过让多个时间、 每次都会请求只能有一个页面调入该驱动程序的兼容性层。 此解决方案可确保每个旧驱动程序将能够处理多个页面的送纸器时调用的 Windows Vista 应用程序中的传输。

（例如用于预览），旧驱动程序可以在传输过程发送"带外"消息。 将忽略这些消息，因为它们不适合的基于流的传输模型。

有关 TYMED 常量的详细信息，请参阅[了解 TYMED](understanding-tymed.md)。

 

 





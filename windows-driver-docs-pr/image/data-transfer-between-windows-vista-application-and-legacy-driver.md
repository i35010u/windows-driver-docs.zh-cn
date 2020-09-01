---
title: 在 Windows Vista 应用程序和旧版驱动程序之间进行的数据传输
description: 在 Windows Vista 应用程序和旧版驱动程序之间进行的数据传输
ms.assetid: 0acb2ca3-6ac6-441d-a12d-446ae5b70295
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3b222d4a1b6e8ce445cd4b68cb390f8e48ba225
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191705"
---
# <a name="data-transfer-between-windows-vista-application-and-legacy-driver"></a>在 Windows Vista 应用程序和旧版驱动程序之间进行的数据传输


使用兼容层，Windows Vista 应用程序可以调用 **IWiaTransfer：:D o) ** (在旧驱动程序的 Microsoft Windows SDK 文档) 中介绍。 兼容性层必须实现文件夹传输代码和格式转换。 兼容性层实现了用于馈送器传输的特殊代码，以确保始终可以从旧驱动程序传输多个页面。 即使使用 TYMED 文件传输，Windows Vista 应用程序也应始终能够在扫描馈送器项期间请求多个页面 \_ 。 下图说明了包含 Windows Vista 应用程序的旧驱动程序。

![演示 windows vista 应用程序和旧驱动程序之间的数据传输的示意图](images/vistaapp-legacydrv.png)

WIA 服务中的旧回调对象将旧传输消息和数据转换为 Windows Vista 传输消息，并将数据写入到提供的流中。

Windows Vista 应用程序只需要 TYMED \_ 文件和 TYMED \_ 多页 \_ 文件，因此兼容性层负责确保 \_ \_ \_ 不会从旧驱动程序向 Windows Vista 应用程序公开 TYMED 回调和 TYMED 多页回调。

实现此部分兼容性层的最简单方法是始终使用 TYMED \_ 文件和 TYMED \_ 多页文件集调入旧驱动程序 \_ 。 执行此操作的缺点是，在将数据写回应用程序的流之前，驱动程序始终需要扫描整个映像。 因此， \_ 当 Windows Vista 应用程序请求 "WIA IPA format" 属性设置为**WiaImgFmt \_ bmp) ** (的 " [**WIA \_ \_ format**](./wia-ipa-format.md) " 属性的扫描时，兼容层将使用 TYMED ** \_ **回调。 这使得兼容层可以通过带区写回数据。

但是，旧的驱动程序不支持 **WiaImgFmt \_ BMP**，而是 **WiaImgFmt \_ MEMORYBMP** for TYMED \_ 回调。 因此，转换回调对象必须创建 BMP 文件头，并将此文件头写入到应用程序。 有时这种情况很简单，如 BMP 文件头可以直接从 BMP info 标头构造。 但在某些情况下，BMP 信息标题的高度设置为0。 在这种情况下，WIA 兼容层必须等待所有数据都已传输完毕，然后才能写入 BMP 文件头并更新 BMP 信息标头。

从旧的驱动程序执行除 TYMED 回调以外的 TYMED 传输的原因 \_ 是，多页格式通常仅受 TYMED \_ 多页文件支持 \_ ，驱动程序通常支持 TYMED 文件的更多格式， \_ 而不是 TYMED \_ 回调。

在 TYMED \_ 文件传输过程中，兼容层会等待传输完成，然后再将数据写回应用程序的流。 这是通过将文件映射到内存并将内存中的所有数据写入一个写入请求来完成的。

在 TYMED \_ 回调传输过程中，每次 \_ \_ 从旧驱动程序收到一条消息数据传输消息时，兼容层都将写回到应用程序的流中。

兼容性层还包含用于送纸器传输的特殊代码。 此代码可确保兼容层可以从 ADF 传输多个页面，即使 TYMED 不是 TYMED 多页 \_ \_ 文件。 完成此操作的方法是：使兼容层多次调用驱动程序，每次只请求一个页面。 此解决方案可确保每个旧的驱动程序在 Windows Vista 应用程序调用时能够处理多个页面的传输。

旧驱动程序可以在传输过程中发送 "带外" 消息 (例如，用于预览) 。 这些消息将被忽略，因为它们不适合基于流的传输模型。

有关 TYMED 常量的详细信息，请参阅 [了解 TYMED](understanding-tymed.md)。

 


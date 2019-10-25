---
title: 将数据传输到 WIA 应用程序
description: 将数据传输到 WIA 应用程序
ms.assetid: 3ad906c9-968f-43d7-ae17-fc570440883d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 601f1c1a982410e27220af651b9a1e253e8fa201
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840730"
---
# <a name="transferring-data-to-a-wia-application"></a>将数据传输到 WIA 应用程序





当应用程序启动数据传输时，WIA 服务将调用[**IWiaMiniDrv：:D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)方法来执行传输。 此方法负责从设备获取数据，并使用[**IWiaMiniDrvCallBack：： MiniDrvCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback)方法将数据发送回应用程序。

在 Microsoft Windows Millennium Edition （Me）和 Windows XP 中，WIA 微型驱动程序应该能够处理两种类型的数据传输：文件和内存。 若要确定应用程序启动的传输类型，微型驱动程序应读取[**WIA\_IPA\_TYMED**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)属性值，或检查[**MINIDRV\_传输\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_minidrv_transfer_context)结构的**TYMED**成员。 仅当 WIA 微型驱动程序调用[**wiasGetImageInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetimageinformation)服务函数时，第二个选项才有效。 **WiasGetImageInformation**服务函数自动读取 WIA\_IPA\_TYMED 属性，并将该值分配给 MINIDRV\_传输\_上下文结构的**TYMED**成员。

首选的方法是，WIA 微型驱动程序读取 WIA\_IPA\_TYMED 属性值。 这可确保微型驱动程序执行正确的购置类型。

从 Windows Vista 开始，引入了一种简化的基于流的传输方法。 有关此数据传输方法的详细信息，请参阅[IStream 数据传输](istream-data-transfers.md)。

本部分包括以下主题：

[了解 TYMED](understanding-tymed.md)

[为数据分配内存](allocating-memory-for-data.md)

[取消数据传输](canceling-a-data-transfer.md)

[取消挂起的 i/o 操作](canceling-pending-i-o-operations.md)

[RAW 格式数据传输](raw-format-data-transfer.md)

有关使用 TYMED （内存中和文件传输）和基于流的传输的数据传输的基本信息，请参阅[数据传输](data-transfers.md)。

 

 





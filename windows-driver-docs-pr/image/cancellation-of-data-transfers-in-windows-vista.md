---
title: 取消 Windows Vista 中的数据传输
description: 取消 Windows Vista 中的数据传输
ms.assetid: 0cdc02bf-23fe-4122-8d5f-f42c3c07da8b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 810002b8f9a68bd69b7cfdee833131e087407567
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840879"
---
# <a name="cancellation-of-data-transfers-in-windows-vista"></a>取消 Windows Vista 中的数据传输


在 Windows Vista 中，应用程序使用**IWiaTransfer** （在 Windows SDK 文档中介绍）来执行基于流的数据传输。 除了新的传输方法，此接口还包含一个可用于取消数据传输的**取消**方法，其中包括[多项传输](multipage-istream-transfers.md)。 使用此方法可以异步取消数据传输。 建议使用此过程取消数据传输。 但是，Windows Vista 应用程序还可以从其回调例程返回\_FALSE，以取消传输。

因此，Windows Vista 中的 WIA 应用程序可以通过两种方式来取消传输：

-   从其回调例程返回\_FALSE。

-   调用**IWiaTransfer：： Cancel**。

Windows Vista 驱动程序可以通过两种不同的方式获得通知：应用程序取消了传输：

-   驱动程序将使用 WIA\_事件接收对其[**IWiaMiniDrv：:D rvnotifypnpevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)的调用，\_CANCEL\_IO 事件。 建议所有内核模式读取或写入操作都使用重叠 i/o。 只有与此过程一起才能保证*立即*取消。

-   从两个回调函数返回了 S @ no__t_0_ FALSE： **IWiaMiniDrvTransferCallback：： GetNextStream**和[**IWiaMiniDrvTransferCallback：： SendMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvtransfercallback-sendmessage)。

当应用程序调用**IWiaTransfer：： Cancel**时，应使用 WIA\_事件将**IWiaMiniDrv：:d rvnotifypnpevent**方法调用到驱动程序中\_取消\_IO。 此外，在取消传输后， [**IWiaMiniDrvTransferCallback：： GetNextStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvtransfercallback-getnextstream)和**IWiaMiniDrvTransferCallback：： SendMessage**回调函数必须始终返回\_FALSE。

如果**IWiaTransferCallback：： GetNextStream**返回 WIA\_状态\_在[多项传输](multipage-istream-transfers.md)过程中跳过\_项，则应用程序将跳过（即不传输）当前项。 S\_的返回值仍然意味着应取消整个传输。

Microsoft Windows SDK 文档中介绍了**IWiaTransfer**和**IWiaTransferCallback**接口。

## <a name="related-topics"></a>相关主题
[**IWiaMiniDrvTransferCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvtransfercallback)  




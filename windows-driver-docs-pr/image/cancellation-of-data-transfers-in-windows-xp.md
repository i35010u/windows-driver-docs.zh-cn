---
title: 取消 Windows XP 中的数据传输
description: 取消 Windows XP 中的数据传输
ms.assetid: 971979a5-950b-49d4-9adb-cd4589a00426
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 414fbae7011ee7d291a184d582c0793816c61a48
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840876"
---
# <a name="cancellation-of-data-transfers-in-windows-xp"></a>取消 Windows XP 中的数据传输


在 Microsoft Windows XP 和 Windows Me 中，WIA 应用程序可以通过两种方式来取消数据传输：

-   从传输回调例程返回\_FALSE， **IWiaDataCallback：： BandedDataCallback**。

-   调用**IWiaItemExtras：： CancelPendingIO**。 不建议使用此方法，它不会被任何内置驱动程序或示例使用。

还有两种方法可以让 WIA 驱动程序通知应用程序已取消传输：

-   在调用[**IWiaMiniDrvCallBack：： MiniDrvCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback)时接收到\_FALSE。

-   使用 WIA\_事件接收对其[ **:D IWiaMiniDrv**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)的调用，\_CANCEL\_IO 事件。

Windows XP 实现的一个问题是，这两种通知方法之间没有连接;也就是说，如果用户调用**IWiaItemExtras：： CancelPendingIO** ，但该驱动程序不支持通过**IWiaMiniDrv：:d rvnotifypnpevent**进行数据传输的异步取消，则该应用程序还必须返回的 **\_FALSEIWiaMiniDrvCallBack：： MiniDrvCallback**<em>。</em>

Microsoft Windows SDK 文档中介绍了**IWiaDataCallback**和**IWiaItemExtras**接口。

 

 





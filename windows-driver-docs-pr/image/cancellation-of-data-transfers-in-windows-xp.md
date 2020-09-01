---
title: 取消 Windows XP 中的数据传输
description: 取消 Windows XP 中的数据传输
ms.assetid: 971979a5-950b-49d4-9adb-cd4589a00426
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2049f13557d51827c5d7ce146bbf62c1fb06c8e0
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192725"
---
# <a name="cancellation-of-data-transfers-in-windows-xp"></a>取消 Windows XP 中的数据传输


在 Microsoft Windows XP 和 Windows Me 中，WIA 应用程序可以通过两种方式来取消数据传输：

-   \_从传输回调例程返回 FALSE， **IWiaDataCallback：： BandedDataCallback**。

-   调用 **IWiaItemExtras：： CancelPendingIO**。 不建议使用此方法，它不会被任何内置驱动程序或示例使用。

还有两种方法可以让 WIA 驱动程序通知应用程序已取消传输：

-   \_如果调用到[**IWiaMiniDrvCallBack：： MiniDrvCallback**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback)，则接收 FALSE。

-   使用 WIA [**IWiaMiniDrv::drvNotifyPnPEvent**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent) \_ 事件 \_ 取消 IO 事件接收对其 IWiaMiniDrv：:d rvnotifypnpevent 的调用 \_ 。

Windows XP 实现的一个问题是，这两种通知方法之间没有连接;也就是说，如果用户调用**IWiaItemExtras：： CancelPendingIO** ，但该驱动程序不支持通过**IWiaMiniDrv：:d rvnotifypnpevent**进行数据传输的异步取消，则该应用程序还必须 \_ 从**IWiaMiniDrvCallBack：： MiniDrvCallback**返回 S FALSE<em>。</em>

Microsoft Windows SDK 文档中介绍了 **IWiaDataCallback** 和 **IWiaItemExtras** 接口。

 


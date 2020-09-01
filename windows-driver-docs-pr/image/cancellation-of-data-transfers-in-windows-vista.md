---
title: 取消 Windows Vista 中的数据传输
description: 取消 Windows Vista 中的数据传输
ms.assetid: 0cdc02bf-23fe-4122-8d5f-f42c3c07da8b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66b212e55ac3f5b55e077e32e1cf1bd439fd078c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192291"
---
# <a name="cancellation-of-data-transfers-in-windows-vista"></a>取消 Windows Vista 中的数据传输


在 Windows Vista 中，有一个新的接口 **IWiaTransfer** (，应用程序使用该接口来执行基于流的数据传输) Windows SDK 文档中所述。 除了新的传输方法，此接口还包含一个可用于取消数据传输的 **取消** 方法，其中包括 [多项传输](multipage-istream-transfers.md)。 使用此方法可以异步取消数据传输。 建议使用此过程取消数据传输。 但是，Windows Vista 应用程序还可以 \_ 从其回调例程返回 FALSE 以取消传输。

因此，Windows Vista 中的 WIA 应用程序可以通过两种方式来取消传输：

-   \_从其回调例程返回 FALSE。

-   调用 **IWiaTransfer：： Cancel**。

Windows Vista 驱动程序可以通过两种不同的方式获得通知：应用程序取消了传输：

-   驱动程序将使用 WIA [**IWiaMiniDrv::drvNotifyPnPEvent**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent) \_ 事件 \_ CANCEL IO 事件接收对其 IWiaMiniDrv：:d rvnotifypnpevent 的调用 \_ 。 建议所有内核模式读取或写入操作都使用重叠 i/o。 只有与此过程一起才能保证 *立即* 取消。

-   S \_ FALSE 从两个回调函数返回： **IWiaMiniDrvTransferCallback：： GetNextStream** 和 [**IWiaMiniDrvTransferCallback：： SendMessage**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvtransfercallback-sendmessage)。

当应用程序调用 **IWiaTransfer：： Cancel**时，应使用 WIA 事件 Cancel IO 将 **IWiaMiniDrv：:d rvnotifypnpevent** 方法调用到驱动程序中 \_ \_ \_ 。 此外，在取消传输后， [**IWiaMiniDrvTransferCallback：： GetNextStream**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvtransfercallback-getnextstream) 和 **IWiaMiniDrvTransferCallback：： SendMessage** 回调函数必须始终返回 S \_ FALSE。

如果 **IWiaTransferCallback：： GetNextStream** \_ \_ \_ 在 [多项传输](multipage-istream-transfers.md)过程中返回 WIA 状态 SKIP 项，应用程序将跳过 (也就是说，不会) 当前项传输。 如果返回值为 \_ FALSE，则表示应取消整个传输。

Microsoft Windows SDK 文档中介绍了 **IWiaTransfer** 和 **IWiaTransferCallback** 接口。

## <a name="related-topics"></a>相关主题
[**IWiaMiniDrvTransferCallback**](/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvtransfercallback)
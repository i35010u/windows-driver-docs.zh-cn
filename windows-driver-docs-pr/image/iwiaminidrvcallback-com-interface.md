---
title: IWiaMiniDrvCallBack COM 接口
description: IWiaMiniDrvCallBack COM 接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 263696a2e6db38617d545d58ba9dff78a3ca513e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799555"
---
# <a name="iwiaminidrvcallback-com-interface"></a>IWiaMiniDrvCallBack COM 接口





[IWiaMiniDrvCallBack 接口](/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)在微型驱动程序和应用程序之间的通信链中提供一个链接。 由于微型驱动程序不能直接与应用程序进行通信，反之亦然，两者之间的任何通信必须通过一个中介： WIA 服务。 若要启用此通信，应用程序需要实现 **IWiaDataCallback** 接口， () 的 Microsoft Windows SDK 文档中所述。 此接口包括 WIA 服务可以调用的 **IWiaDataCallback：： BandedDataCallback** 方法。 如果某个应用程序提供此回调例程，WIA 服务将创建另一个回调，该回调是它提供给微型驱动程序使用的 [**IWiaMiniDrvCallBack：： MiniDrvCallback**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback) 方法。

当微型驱动程序准备好从映像设备发送图像数据或传输状态消息 (传输的数据百分比（例如) ）时，它将调用 WIA 服务的 **IWiaMiniDrvCallBack**：：**MiniDrvCallback**。 然后，在调用应用程序的回调时，WIA 服务会将数据或消息传递给应用程序。

 


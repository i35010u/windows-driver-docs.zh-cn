---
title: IWiaMiniDrvCallBack COM 接口
description: IWiaMiniDrvCallBack COM 接口
ms.assetid: a535d718-e34f-4cd0-9137-83d28d0b8e9c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: baf662ac75dd21b8f33fa347cc87fbc8ba5abc1f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840794"
---
# <a name="iwiaminidrvcallback-com-interface"></a>IWiaMiniDrvCallBack COM 接口





[IWiaMiniDrvCallBack 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)在微型驱动程序和应用程序之间的通信链中提供一个链接。 由于微型驱动程序不能直接与应用程序进行通信，反之亦然，两者之间的任何通信必须通过一个中介： WIA 服务。 若要启用此通信，应用程序需要实现**IWiaDataCallback**接口（如 Microsoft Windows SDK 文档中所述）。 此接口包括 WIA 服务可以调用的**IWiaDataCallback：： BandedDataCallback**方法。 如果某个应用程序提供此回调例程，WIA 服务将创建另一个回调，该回调是它提供给微型驱动程序使用的[**IWiaMiniDrvCallBack：： MiniDrvCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback)方法。

当微型驱动程序准备好从图像设备发送图像数据或传输状态消息（例如，传输的数据的百分比）时，它将调用 WIA 服务的**IWiaMiniDrvCallBack**：：**MiniDrvCallback**。 然后，在调用应用程序的回调时，WIA 服务会将数据或消息传递给应用程序。

 

 





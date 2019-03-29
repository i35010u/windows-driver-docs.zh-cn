---
title: 取消 Windows Vista 中的数据传输
description: 取消 Windows Vista 中的数据传输
ms.assetid: 0cdc02bf-23fe-4122-8d5f-f42c3c07da8b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7a456ee86ca7245cb4d2823abbd24c588150588
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567086"
---
# <a name="cancellation-of-data-transfers-in-windows-vista"></a>取消 Windows Vista 中的数据传输


在 Windows Vista 中，没有新接口**IWiaTransfer** （其中描述了 Windows SDK 文档中） 应用程序用来执行基于流的数据传输。 除了新的传输方法，此接口包含**取消**方法，该应用程序可以使用取消数据传输，包括方法[多项传输](multipage-istream-transfers.md)。 使用此方法，您可以以异步方式取消数据传输。 我们建议使用此过程来取消数据传输。 但是，Windows Vista 应用程序还可以返回 S\_FALSE 从其回调例程，以取消传输。

因此，有两种方法 WIA 应用程序在 Windows Vista 中可以取消传输：

-   返回 S\_FALSE 从其回调例程。

-   调用**IWiaTransfer::Cancel**。

Windows Vista 驱动程序可以通知应用程序已取消传输的两种不同方式：

-   该驱动程序接收到调用其[ **IWiaMiniDrv::drvNotifyPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff544998)使用 WIA\_事件\_取消\_IO 事件。 我们建议所有内核模式下都读取或写入操作使用重叠 I/O。 使用此过程仅保证*即时*取消。

-   S\_从两个回调函数返回 FALSE:**IWiaMiniDrvTransferCallback::GetNextStream**并[ **IWiaMiniDrvTransferCallback::SendMessage**](https://msdn.microsoft.com/library/windows/hardware/jj151552)。

当应用程序调用**IWiaTransfer::Cancel**，则**IWiaMiniDrv::drvNotifyPnPEvent**方法应调用到驱动程序和 WIA\_事件\_取消\_IO。 此外， [ **IWiaMiniDrvTransferCallback::GetNextStream** ](https://msdn.microsoft.com/library/windows/hardware/jj151551)并**IWiaMiniDrvTransferCallback::SendMessage**回调函数必须始终返回 S\_已取消传输后，则为 FALSE。

如果**IWiaTransferCallback::GetNextStream**返回 WIA\_状态\_跳过\_项期间[多项传输](multipage-istream-transfers.md)，应用程序将跳过 (即，不正在传输） 的当前项。 返回值为 S\_FALSE 仍意味着应取消整个传输。

**IWiaTransfer**并**IWiaTransferCallback**接口 Microsoft Windows SDK 文档中所述。

## <a name="related-topics"></a>相关主题
[**IWiaMiniDrvTransferCallback**](https://msdn.microsoft.com/library/windows/hardware/jj151550)  




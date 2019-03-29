---
title: 取消 Windows XP 中的数据传输
description: 取消 Windows XP 中的数据传输
ms.assetid: 971979a5-950b-49d4-9adb-cd4589a00426
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6741c9564485a42ca0753be033d9542422c9b38
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561999"
---
# <a name="cancellation-of-data-transfers-in-windows-xp"></a>取消 Windows XP 中的数据传输


在 Microsoft Windows XP 和 Windows Me 中，没有 WIA 应用程序可以取消数据传输的两种方法：

-   返回 S\_传输回调例程，FALSE **IWiaDataCallback::BandedDataCallback**。

-   调用**IWiaItemExtras::CancelPendingIO**。 我们不建议此方法，它不由任何现成的驱动程序或示例。

此外提供了两种 WIA 驱动程序应用程序，必须取消传输接收通知的方法：

-   收到 S\_FALSE 时调用了[ **IWiaMiniDrvCallBack::MiniDrvCallback**](https://msdn.microsoft.com/library/windows/hardware/ff543946)。

-   接收到调用其[ **IWiaMiniDrv::drvNotifyPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff544998)使用 WIA\_事件\_取消\_IO 事件。

与 Windows XP 实现的一个问题是两个通知方法; 这些方法之间没有连接也就是说，如果用户调用**IWiaItemExtras::CancelPendingIO** ，但该驱动程序不支持通过数据传输的异步取消**IWiaMiniDrv::drvNotifyPnPEvent**，将应用程序此外必须返回 S\_从 FALSE **IWiaMiniDrvCallBack::MiniDrvCallback**<em>。</em>

**IWiaDataCallback**并**IWiaItemExtras**接口 Microsoft Windows SDK 文档中所述。

 

 





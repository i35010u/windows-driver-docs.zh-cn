---
title: WIA 错误处理程序取消无模式对话框
description: WIA 错误处理程序取消无模式对话框
ms.assetid: eca6c3a3-c196-4d28-925a-c8f5d5d8601b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a4f71fd5122fbd8f36f4c182b3cf6b2f9869271
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840699"
---
# <a name="wia-error-handler-cancellation-of-modeless-dialogs"></a>WIA 错误处理程序取消无模式对话框


错误处理程序中的许多复杂性都围绕如何处理无模式对话框的取消和消除。

特别是，WIA 代理代码确保较低级别的错误处理程序（换言之，不是该应用程序的错误处理程序的处理程序）可以将取消请求从无模式对话框传回驱动程序;这可确保较低级别的处理程序有机会取消其无模式对话框。

为了使错误处理程序能够取消无模式对话框中的数据传输操作，驱动程序应始终发送 WIA\_\_传输\_设备\_状态消息与相同的*hrErrorStatus*代码，这可能是更新*lPercentComplete*参数以允许错误处理程序 UI 显示进度。 例如，如果驱动程序可以估计 "预热" 所用的时间，则它可以发送多个*hrErrorStatus*设置为 WIA\_状态\_预热\_的设备消息。 这将允许错误处理程序显示进度对话框，并为用户提供从该对话框取消传输的机会。 传递到[**IWiaErrorHandler：： ReportStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiaerrorhandler-reportstatus)的*lPercentComplete*参数是驱动程序在**IWiaTransferCallback：： WiaTransferParams**方法中设置的完全相同的*lPercentComplete*参数。 有关这种情况的示例，请参阅 WDK CD 上的扩展 WIA 怪物驱动程序。

为了允许错误处理程序消除无模式对话框，Microsoft 引入了设备状态代码 WIA\_状态\_清除。 当 WIA 代理接收到来自当前正在显示的设备消息的其他设备消息时，WIA 代理会将此消息发送到当前显示无模式 UI 的错误处理程序。 当以下情况时，代理还会将 WIA\_状态\_明文消息：

驱动程序发送 WIA\_传输\_消息\_状态消息，

在调用**IWiaTransferCallback：： GetNextStream**方法期间

流/传输结束时（如果当前存在显示无模式 UI 的错误处理程序）。

驱动程序不应将 WIA\_状态发送\_明文消息本身。

Microsoft Windows SDK 文档中介绍了**IWiaTransferCallback**接口。

 

 





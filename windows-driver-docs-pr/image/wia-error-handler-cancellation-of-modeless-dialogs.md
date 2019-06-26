---
title: WIA 错误处理程序取消无模式对话框
description: WIA 错误处理程序取消无模式对话框
ms.assetid: eca6c3a3-c196-4d28-925a-c8f5d5d8601b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89b8e285cb1003ab04e0c50e040b8bd1dc34dbe5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383758"
---
# <a name="wia-error-handler-cancellation-of-modeless-dialogs"></a>WIA 错误处理程序取消无模式对话框


中的错误处理程序的复杂性大部分围绕如何处理取消和上诉无模式对话框。

具体而言，WIA 代理代码可确保较低级别的错误处理程序 （即该应用程序的错误处理程序之外的处理程序） 获取机会通信对驱动程序; 从无模式对话框返回的取消请求这可确保较低级别的处理程序有机会关闭其无模式对话框。

若要允许错误处理程序来取消数据传输操作中的从无模式对话框，驱动程序应保留发送的 WIA\_传输\_MSG\_设备\_具有相同的状态消息*hrErrorStatus*代码中，可能更新*lPercentComplete*参数，以允许错误处理程序 UI 以显示进度。 例如，如果驱动程序可以如何估计长时间"热身"真正采用，它可以发送的设备的消息数*hrErrorStatus*设置为 WIA\_状态\_WARMING\_向上。 这将允许错误处理程序，以显示进度对话框，以及为用户提供取消此对话框从传输的机会。 *LPercentComplete*参数传递到[ **IWiaErrorHandler::ReportStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nf-wia_lh-iwiaerrorhandler-reportstatus)相当精确*lPercentComplete*驱动程序设置中的参数**IWiaTransferCallback::WiaTransferParams**方法。 此示例，请参阅 WDK CD 上的扩展 WIA 这头怪兽驱动程序。

若要允许错误处理程序，关闭无模式对话框，Microsoft 推出的设备状态代码 WIA\_状态\_清除。 WIA 代理情况下，此消息发送到当前正在显示无模式的 UI 时 WIA 代理接收不同的设备消息从当前显示的错误处理程序。 代理还会发送 WIA\_状态\_清除消息时：

驱动程序将发送出 WIA\_传输\_消息\_状态消息

在调用期间**IWiaTransferCallback::GetNextStream**方法

在流/传输 （如果当前没有错误处理程序显示无模式 UI） 的末尾。

驱动程序不应发送 WIA\_状态\_清除消息本身。

**IWiaTransferCallback** Microsoft Windows SDK 文档中详细介绍了接口。

 

 





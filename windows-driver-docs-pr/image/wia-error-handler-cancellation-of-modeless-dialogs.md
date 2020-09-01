---
title: WIA 错误处理程序取消无模式对话框
description: WIA 错误处理程序取消无模式对话框
ms.assetid: eca6c3a3-c196-4d28-925a-c8f5d5d8601b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78ac4958355cd42f83b4b81484410138593666bc
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185009"
---
# <a name="wia-error-handler-cancellation-of-modeless-dialogs"></a>WIA 错误处理程序取消无模式对话框


错误处理程序中的许多复杂性都围绕如何处理无模式对话框的取消和消除。

特别是，WIA 代理代码确保较低级别的错误处理程序 (换言之，而不是该应用程序的错误处理程序的处理程序) 获取机会将取消请求从无模式对话框传回驱动程序;这可确保较低级别的处理程序有机会取消其无模式对话框。

为了使错误处理程序能够取消无模式对话框中的数据传输操作，驱动程序应 \_ \_ 使用相同的 hrErrorStatus 代码来继续发送 WIA 传输消息 \_ 设备 \_ 状态*hrErrorStatus*消息，这可能会更新*LPERCENTCOMPLETE*参数以允许错误处理程序 UI 显示进度。 例如，如果驱动程序可以估计 "预热" 所用的时间，则它可以发送多个 *hrErrorStatus* 设置为 WIA 状态预热的设备消息 \_ \_ \_ 。 这将允许错误处理程序显示进度对话框，并为用户提供从该对话框取消传输的机会。 传递到[**IWiaErrorHandler：： ReportStatus**](/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiaerrorhandler-reportstatus)的*lPercentComplete*参数是驱动程序在**IWiaTransferCallback：： WiaTransferParams**方法中设置的完全相同的*lPercentComplete*参数。 有关这种情况的示例，请参阅 WDK CD 上的扩展 WIA 怪物驱动程序。

为了允许错误处理程序消除无模式对话框，Microsoft 引入了设备状态代码 WIA \_ 状态 " \_ 清除"。 当 WIA 代理接收到来自当前正在显示的设备消息的其他设备消息时，WIA 代理会将此消息发送到当前显示无模式 UI 的错误处理程序。 代理还会 \_ \_ 在以下情况发送 WIA 状态明文消息：

驱动程序发送 WIA \_ 传输 \_ 消息 \_ 状态消息，

在调用 **IWiaTransferCallback：： GetNextStream** 方法期间

如果当前存在显示无模式 UI) 的错误处理程序，则在流/传输 (末尾。

驱动程序不应发送 WIA \_ 状态 \_ 清除消息本身。

Microsoft Windows SDK 文档中介绍了 **IWiaTransferCallback** 接口。

 


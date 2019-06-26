---
title: 如何 WIA 微型驱动程序收到断开 WIA
description: WIA 微型驱动程序如何从 WIA 服务接收断开连接事件
ms.assetid: 6ae3c230-d026-469e-a699-860a295fba85
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 417cf2089c4e0adf9edfd92162d10fd3ea1273d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363056"
---
# <a name="how-the-wia-minidriver-receives-a-disconnect-event-from-the-wia-service"></a>WIA 微型驱动程序如何从 WIA 服务接收断开连接事件

当设备意外断开连接的计算机，例如当用户断开 USB 电缆连接在计算机中，从 WIA 服务调用[ **IWiaMiniDrv::drvNotifyPnpEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)方法WIA\_事件\_设备\_DISCONNECTED 的事件。 请参阅[添加中断事件支持](adding-interrupt-event-support.md)有关的示例实现**IWiaMiniDrv::drvNotifyPnpEvent**方法。

WIA 微型驱动程序不应尝试期间或之后此事件与硬件通信。 此事件指示 WIA 服务将卸载微型驱动程序。 当 WIA 服务将重新加载微型驱动程序时，允许的下一步的设备访问权限。 建议微型驱动程序将设置一个标志，该标志阻止所有[IWiaMiniDrv](iwiaminidrv-com-interface.md)接口从访问硬件，直到重新连接后调用。

WIA\_事件\_设备\_DISCONNECTED 的事件始终未发送到 WIA 微型驱动程序。 当计算机正在关闭并 WIA 服务正在卸载 WIA 驱动程序时，不发送此事件。 此事件应视为禁用操作的设备硬件。

 




---
title: 提供事件通知
description: 提供事件通知
ms.assetid: 53ca7ef0-fa8b-4ae1-9b5e-b145c2d02db2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de12f74604ee0a9682761b2aa57e1a3d31227c34
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187603"
---
# <a name="providing-event-notification"></a>提供事件通知





WIA 服务通过调用 [**IWiaMiniDrv：:D rvnotifypnpevent**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent) 方法，将支持的设备事件的 wia 微型驱动程序通知。 在此方法中，微型驱动程序实现响应事件所需的特定于设备的功能。 WIA 服务仅对微型驱动程序表明设备可以在[**IWiaMiniDrv：:D rvgetcapabilities**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)方法中支持的事件调用**IWiaMiniDrv：:d rvnotifypnpevent**方法。

微型驱动程序通过 STI 事件机制启动事件，或使用 [**wiasQueueEvent**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasqueueevent) 将事件通知从此设备添加到事件队列。

### <a name="asynchronous-behavior-power-management-and-io-cancellation"></a>异步行为：电源管理和 i/o 取消

在大多数情况下，WIA 服务确保每次只能对驱动程序进行一次调用。 但是，某些方法在本质上是异步和可重入的。 这是一个很好的例子，就是 [**IWiaMiniDrv：:D rvnotifypnpevent**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent) 方法。

WIA 服务使用此方法通知驱动程序可能需要立即操作的事件。 例如，当 WIA 服务收到一个指示设备已被删除的即插即用事件时，它会立即通知驱动程序。 其他示例包括应用程序中的电源管理事件和 i/o 取消请求。

有关 [**IWiaMiniDrv：:D rvnotifypnpevent**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent) 方法的示例实现，阐释了应如何响应各种事件，请参阅 [添加中断事件支持](adding-interrupt-event-support.md)。

 


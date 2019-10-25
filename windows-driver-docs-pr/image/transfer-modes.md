---
title: 传输模式
description: 传输模式
ms.assetid: 79af0d8f-dd04-4ff4-a047-f415562a16a5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59e858b0d2d4d45612f393f3c1887031194142c4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840735"
---
# <a name="transfer-modes"></a>传输模式





静止图像接口定义两种传输模式−*状态模式*和*数据模式*。 当**IStillImage** COM 接口的客户端调用[**IStillImage：： CreateDevice**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543778(v=vs.85))来获取对静止图像设备的访问权限时，它将指定传输模式的一个（或两个）。 多个客户端可以在状态模式下打开设备，但是一次只允许一个客户端在数据模式中打开设备。

静止图像事件监视器在状态模式下打开设备。 通常（但不总是）[图像获取 api](creating-device-specific-components-for-image-acquisition-apis.md)在数据模式中打开设备。

当客户端在数据模式中打开设备后，事件监视器会将后续的[静止图像设备事件](still-image-device-events.md)存储在内部队列中。 如果客户端调用[**IStiDevice：：订阅**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-subscribe)，它可以通过调用[**IStiDevice：： GetLastNotificationData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getlastnotificationdata)从队列中读取事件。 客户端关闭设备后，随后收到的事件将导致事件监视器再次尝试启动已注册的应用程序。

两种传输模式的含义完全取决于设备的用户模式微型驱动程序。 **IStillImage**和**IStiDevice**接口允许在任一模式下调用所有方法。

微型驱动程序可以通过调用[**IStiDevice：： GetLastNotificationData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getlastnotificationdata)来确定它的打开模式。 如果客户端在获取设备访问权限时只请求了状态模式，则微型驱动程序应禁止客户端执行数据传输。

务必要注意的是，在相对较长的时间（例如，事件监视器会监视设备事件）以状态模式打开设备时，在相对较短的时间（例如，读取图像）以数据模式打开设备。 虽然静止映像体系结构一次只允许一个客户端在数据模式中打开设备，但驱动程序可能需要对设备访问进行进一步的限制。

例如，如果要为连接到串行端口的设备编写驱动程序，则可能需要从驱动程序的[**IStiUSD：： LockDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-lockdevice)方法中调用[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea) （如果设备在状态模式下打开）。 这将禁止其他应用程序使用该端口（可能支持其他设备），同时从设备获取状态信息。

对于连接到专用端口（如 SCSI 或 USB 总线设备）的设备，通常允许从[**IStiUSD：： Initialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)内调用[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea) ，前提是指定了状态模式，因为设备和端口将始终专用于一个机.

在数据模式中打开设备时， [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)通常从**IStiUSD： Initialize**内调用，而与总线类型无关。

 

 





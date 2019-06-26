---
title: 传输模式
description: 传输模式
ms.assetid: 79af0d8f-dd04-4ff4-a047-f415562a16a5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81704a52aff4ad3f27fc15c440e49ca136cd54c9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358229"
---
# <a name="transfer-modes"></a>传输模式





静止图像接口定义两个传输模式 −*状态模式*并*数据模式*。 时的客户端**IStillImage** COM 接口调用[ **IStillImage::CreateDevice** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543778(v=vs.85))若要获取对静止图像设备的访问，它指定一个 （或两者） 传输模式。 多个客户端可以在状态模式下，打开设备，但一次只有一个客户端允许在数据模式下打开设备。

静止图像事件监视器状态模式中打开设备。 通常情况下，但不是总是[图像采集 Api](creating-device-specific-components-for-image-acquisition-apis.md)在数据模式下打开设备。

事件监视器后客户端在数据模式中打开设备、 存储后续[静止图像的设备事件](still-image-device-events.md)内部队列中。 如果客户端调用[ **IStiDevice::Subscribe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-subscribe)，它可以从队列读取事件，通过调用[ **IStiDevice::GetLastNotificationData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getlastnotificationdata). 客户端关闭设备后，随后接收的事件会导致事件监视器以再次尝试启动已注册的应用程序。

两个传输模式的含义是完全取决于设备的用户模式下微型驱动程序。 **IStillImage**并**IStiDevice**接口允许调用任何一种模式中的所有方法。

微型驱动程序可以确定它已打开通过调用的模式[ **IStiDevice::GetLastNotificationData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getlastnotificationdata)。 微型驱动程序应禁止在客户端执行数据传输，如果获取设备的访问权限时，客户端请求状态模式。

务必要注意的设备通常在相对较长的状态模式中打开时在数据模式中为相对较短的时间 （例如，若要在图像中读取） 的打开时间 （例如，设备事件的事件监视器监视文件）。 尽管仍映像体系结构允许在数据模式下打开设备一次只有一个客户端，但可能有必要进行进一步限制设备访问的驱动程序。

例如，如果你正在编写用于连接到串行端口的设备的驱动程序，你可能想要调用[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)从中的驱动程序[ **IStiUSD::LockDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-lockdevice)方法如果设备已在状态模式下打开。 这将阻止其他应用程序从状态时使用的端口 （这可能支持其他设备） 从设备中获得的信息。

连接到专用端口，例如 SCSI 或 USB 总线设备的设备，通常允许调用[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)中[ **IStiUSD::Initialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-initialize)如果状态模式指定了，因为设备和端口始终将专用于一台客户端。

在数据模式中，打开设备时[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)通常称为内部**IStiUSD:Initialize**、 总线类型无关。

 

 





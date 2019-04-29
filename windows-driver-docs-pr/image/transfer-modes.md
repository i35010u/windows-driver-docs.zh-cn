---
title: 传输模式
description: 传输模式
ms.assetid: 79af0d8f-dd04-4ff4-a047-f415562a16a5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b1238a65de397dbf32e684cf10afb226e65ba3f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389610"
---
# <a name="transfer-modes"></a>传输模式





静止图像接口定义两个传输模式 −*状态模式*并*数据模式*。 时的客户端**IStillImage** COM 接口调用[ **IStillImage::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff543778)若要获取对静止图像设备的访问，它指定一个 （或两者） 传输模式。 多个客户端可以在状态模式下，打开设备，但一次只有一个客户端允许在数据模式下打开设备。

静止图像事件监视器状态模式中打开设备。 通常情况下，但不是总是[图像采集 Api](creating-device-specific-components-for-image-acquisition-apis.md)在数据模式下打开设备。

事件监视器后客户端在数据模式中打开设备、 存储后续[静止图像的设备事件](still-image-device-events.md)内部队列中。 如果客户端调用[ **IStiDevice::Subscribe**](https://msdn.microsoft.com/library/windows/hardware/ff543768)，它可以从队列读取事件，通过调用[ **IStiDevice::GetLastNotificationData** ](https://msdn.microsoft.com/library/windows/hardware/ff543751). 客户端关闭设备后，随后接收的事件会导致事件监视器以再次尝试启动已注册的应用程序。

两个传输模式的含义是完全取决于设备的用户模式下微型驱动程序。 **IStillImage**并**IStiDevice**接口允许调用任何一种模式中的所有方法。

微型驱动程序可以确定它已打开通过调用的模式[ **IStiDevice::GetLastNotificationData**](https://msdn.microsoft.com/library/windows/hardware/ff543751)。 微型驱动程序应禁止在客户端执行数据传输，如果获取设备的访问权限时，客户端请求状态模式。

务必要注意的设备通常在相对较长的状态模式中打开时在数据模式中为相对较短的时间 （例如，若要在图像中读取） 的打开时间 （例如，设备事件的事件监视器监视文件）。 尽管仍映像体系结构允许在数据模式下打开设备一次只有一个客户端，但可能有必要进行进一步限制设备访问的驱动程序。

例如，如果你正在编写用于连接到串行端口的设备的驱动程序，你可能想要调用[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)从中的驱动程序[ **IStiUSD::LockDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff543829)方法如果设备已在状态模式下打开。 这将阻止其他应用程序从状态时使用的端口 （这可能支持其他设备） 从设备中获得的信息。

连接到专用端口，例如 SCSI 或 USB 总线设备的设备，通常允许调用[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)中[ **IStiUSD::Initialize**](https://msdn.microsoft.com/library/windows/hardware/ff543824)如果状态模式指定了，因为设备和端口始终将专用于一台客户端。

在数据模式中，打开设备时[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)通常称为内部**IStiUSD:Initialize**、 总线类型无关。

 

 





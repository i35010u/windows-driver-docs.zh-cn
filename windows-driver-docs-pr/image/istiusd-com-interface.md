---
title: IStiUSD COM 接口
description: IStiUSD COM 接口
ms.assetid: 2f805955-8c66-4c9e-839e-c8a98c6637a8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b1d3cd7e998ef0c761936826b580db47ddb500a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186465"
---
# <a name="istiusd-com-interface"></a>IStiUSD COM 接口





**IStiUSD** com 接口是[IStiDevice com 接口](istidevice-com-interface.md)与静态图像设备通信的方式。 **IStiUSD**接口的方法由供应商提供的每个[用户模式静止图像微型驱动程序](overview-of-sti-components.md#ddk-user-mode-still-image-minidrivers-si)实现。

通常， **IStiUSD** 接口方法由 **IStiDevice** 接口定义的名称类似的方法调用。 静止图像微型驱动程序通常通过调用相应的内核模式驱动程序来实现 **IStiUSD** 接口方法。 每个微型驱动程序都必须定义所有接口方法，但如果不需要方法，它可以返回 \_ 不支持的 STIERR。

**IStiUSD**接口定义的方法包括：

<a href="" id="istiusd--devicereset"></a>[**IStiUSD：:D eviceReset**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-devicereset)  
将静止图像设备重置为已知的初始化状态。

<a href="" id="istiusd--diagnostic"></a>[**IStiUSD：:D 诊断**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-diagnostic)  
在静止图像设备上运行诊断测试。

<a href="" id="istiusd--escape"></a>[**IStiUSD：： Escape**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-escape)  
对静止图像设备执行特定于供应商的 i/o 操作。

<a href="" id="istiusd--getcapabilities"></a>[**IStiUSD：： GetCapabilities**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getcapabilities)  
返回静止图像设备的功能。

<a href="" id="istiusd--getlasterrorinfo"></a>[**IStiUSD::GetLastErrorInfo**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getlasterrorinfo)  
返回有关与静态图像设备关联的上一个已知错误的信息。

<a href="" id="istiusd--getnotificationdata"></a>[**IStiUSD::GetNotificationData**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getnotificationdata)  
返回在静止图像设备上发生的最近事件的说明。

<a href="" id="istiusd--getstatus"></a>[**IStiUSD：： GetStatus**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getstatus)  
返回静止图像设备的状态。

<a href="" id="istiusd--initialize"></a>[**IStiUSD：： Initialize**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)  
初始化定义 **IStiUSD** 接口的 COM 对象的实例。

<a href="" id="istiusd--lockdevice"></a>[**IStiUSD::LockDevice**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-lockdevice)  
锁定设备以供调用方独占使用。

<a href="" id="istiusd--rawreadcommand"></a>**IStiUSD::RawReadCommand**  
从静态图像设备读取命令信息。

<a href="" id="istiusd--rawreaddata"></a>[**IStiUSD::RawReadData**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawreaddata)  
从静止图像设备读取数据。

<a href="" id="istiusd--rawwritecommand"></a>[**IStiUSD::RawWriteCommand**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawwritecommand)  
向静止图像设备写入命令信息。

<a href="" id="istiusd--rawwritedata"></a>[**IStiUSD::RawWriteData**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawwritedata)  
将数据写入静止图像设备。

<a href="" id="istiusd--setnotificationhandle"></a>[**IStiUSD::SetNotificationHandle**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-setnotificationhandle)  
指定微型驱动程序应用于向调用方通知设备事件的事件句柄。 通常由静态图像事件监视器调用。

<a href="" id="istiusd--unlockdevice"></a>[**IStiUSD::UnLockDevice**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-unlockdevice)  
解锁设备。

 


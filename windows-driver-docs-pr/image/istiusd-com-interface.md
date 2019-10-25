---
title: IStiUSD COM 接口
description: IStiUSD COM 接口
ms.assetid: 2f805955-8c66-4c9e-839e-c8a98c6637a8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 412beac255f6be463bb8b8b6cb51c606b41d1fc5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840807"
---
# <a name="istiusd-com-interface"></a>IStiUSD COM 接口





**IStiUSD** com 接口是[IStiDevice com 接口](istidevice-com-interface.md)与静态图像设备通信的方式。 **IStiUSD**接口的方法由供应商提供的每个[用户模式静止图像微型驱动程序](overview-of-sti-components.md#ddk-user-mode-still-image-minidrivers-si)实现。

通常， **IStiUSD**接口方法由**IStiDevice**接口定义的名称类似的方法调用。 静止图像微型驱动程序通常通过调用相应的内核模式驱动程序来实现**IStiUSD**接口方法。 每个微型驱动程序都必须定义所有接口方法，但如果不需要某个方法，则可以返回不受支持的 STIERR\_。

**IStiUSD**接口定义的方法包括：

<a href="" id="istiusd--devicereset"></a>[**IStiUSD：:D eviceReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-devicereset)  
将静止图像设备重置为已知的初始化状态。

<a href="" id="istiusd--diagnostic"></a>[**IStiUSD：:D 诊断**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-diagnostic)  
在静止图像设备上运行诊断测试。

<a href="" id="istiusd--escape"></a>[**IStiUSD：： Escape**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-escape)  
对静止图像设备执行特定于供应商的 i/o 操作。

<a href="" id="istiusd--getcapabilities"></a>[**IStiUSD：： GetCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getcapabilities)  
返回静止图像设备的功能。

<a href="" id="istiusd--getlasterrorinfo"></a>[**IStiUSD::GetLastErrorInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getlasterrorinfo)  
返回有关与静态图像设备关联的上一个已知错误的信息。

<a href="" id="istiusd--getnotificationdata"></a>[**IStiUSD::GetNotificationData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getnotificationdata)  
返回在静止图像设备上发生的最近事件的说明。

<a href="" id="istiusd--getstatus"></a>[**IStiUSD：： GetStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getstatus)  
返回静止图像设备的状态。

<a href="" id="istiusd--initialize"></a>[**IStiUSD：： Initialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)  
初始化定义**IStiUSD**接口的 COM 对象的实例。

<a href="" id="istiusd--lockdevice"></a>[**IStiUSD::LockDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-lockdevice)  
锁定设备以供调用方独占使用。

<a href="" id="istiusd--rawreadcommand"></a>**IStiUSD::RawReadCommand**  
从静态图像设备读取命令信息。

<a href="" id="istiusd--rawreaddata"></a>[**IStiUSD::RawReadData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawreaddata)  
从静止图像设备读取数据。

<a href="" id="istiusd--rawwritecommand"></a>[**IStiUSD::RawWriteCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawwritecommand)  
向静止图像设备写入命令信息。

<a href="" id="istiusd--rawwritedata"></a>[**IStiUSD::RawWriteData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawwritedata)  
将数据写入静止图像设备。

<a href="" id="istiusd--setnotificationhandle"></a>[**IStiUSD::SetNotificationHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-setnotificationhandle)  
指定微型驱动程序应用于向调用方通知设备事件的事件句柄。 通常由静态图像事件监视器调用。

<a href="" id="istiusd--unlockdevice"></a>[**IStiUSD::UnLockDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-unlockdevice)  
解锁设备。

 

 





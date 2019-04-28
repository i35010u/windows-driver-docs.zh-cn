---
title: IStiUSD COM 接口
description: IStiUSD COM 接口
ms.assetid: 2f805955-8c66-4c9e-839e-c8a98c6637a8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea4f4f5b4670df9aff4a33719d5d0904c22f1ce7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327451"
---
# <a name="istiusd-com-interface"></a>IStiUSD COM 接口





**IStiUSD** COM 接口是方式的情况[IStiDevice COM 接口](istidevice-com-interface.md)与静止图像设备进行通信。 **IStiUSD**接口的方法实现的每个供应商提供[用户模式下仍映像微型驱动程序](overview-of-sti-components.md#ddk-user-mode-still-image-minidrivers-si)。

通常情况下， **IStiUSD**定义的命名方式类似的方法调用接口方法**IStiDevice**接口。 通常情况下实现映像微型驱动程序仍**IStiUSD**接口方法通过调用适当的内核模式驱动程序。 每个微型驱动程序必须定义接口中的所有方法，但如果方法不需要它可以返回 STIERR\_不受支持。

由定义的方法**IStiUSD**接口包括以下：

<a href="" id="istiusd--devicereset"></a>[**IStiUSD::DeviceReset**](https://msdn.microsoft.com/library/windows/hardware/ff543812)  
将静态图像设备重置到已知的初始化状态。

<a href="" id="istiusd--diagnostic"></a>[**IStiUSD::Diagnostic**](https://msdn.microsoft.com/library/windows/hardware/ff543814)  
在静态图像设备上运行诊断测试。

<a href="" id="istiusd--escape"></a>[**IStiUSD::Escape**](https://msdn.microsoft.com/library/windows/hardware/ff543815)  
执行静态图像设备上的特定于供应商的 I/O 操作。

<a href="" id="istiusd--getcapabilities"></a>[**IStiUSD::GetCapabilities**](https://msdn.microsoft.com/library/windows/hardware/ff543817)  
返回一个静态的图像设备的功能。

<a href="" id="istiusd--getlasterrorinfo"></a>[**IStiUSD::GetLastErrorInfo**](https://msdn.microsoft.com/library/windows/hardware/ff543820)  
返回有关与静态图像设备相关联的最后一个已知错误的信息。

<a href="" id="istiusd--getnotificationdata"></a>[**IStiUSD::GetNotificationData**](https://msdn.microsoft.com/library/windows/hardware/ff543821)  
返回的静态图像设备发生的最新事件的描述。

<a href="" id="istiusd--getstatus"></a>[**IStiUSD::GetStatus**](https://msdn.microsoft.com/library/windows/hardware/ff543823)  
返回静态图像设备的状态。

<a href="" id="istiusd--initialize"></a>[**IStiUSD::Initialize**](https://msdn.microsoft.com/library/windows/hardware/ff543824)  
初始化一个实例定义的 COM 对象**IStiUSD**接口。

<a href="" id="istiusd--lockdevice"></a>[**IStiUSD::LockDevice**](https://msdn.microsoft.com/library/windows/hardware/ff543829)  
锁定供独占使用由调用方的设备。

<a href="" id="istiusd--rawreadcommand"></a>**IStiUSD::RawReadCommand**  
读取命令从静态图像设备信息。

<a href="" id="istiusd--rawreaddata"></a>[**IStiUSD::RawReadData**](https://msdn.microsoft.com/library/windows/hardware/ff543834)  
从静态图像设备读取数据。

<a href="" id="istiusd--rawwritecommand"></a>[**IStiUSD::RawWriteCommand**](https://msdn.microsoft.com/library/windows/hardware/ff543836)  
写入静态图像设备命令的信息。

<a href="" id="istiusd--rawwritedata"></a>[**IStiUSD::RawWriteData**](https://msdn.microsoft.com/library/windows/hardware/ff543839)  
将数据写入到静态图像设备。

<a href="" id="istiusd--setnotificationhandle"></a>[**IStiUSD::SetNotificationHandle**](https://msdn.microsoft.com/library/windows/hardware/ff543840)  
指定应使用微型驱动程序通知设备事件的调用方的事件句柄。 通常由静止图像事件监视器调用。

<a href="" id="istiusd--unlockdevice"></a>[**IStiUSD::UnLockDevice**](https://msdn.microsoft.com/library/windows/hardware/ff543843)  
解锁设备。

 

 





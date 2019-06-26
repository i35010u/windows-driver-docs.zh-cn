---
title: IStiDeviceControl COM 接口
description: IStiDeviceControl COM 接口
ms.assetid: 6d98f5d7-c471-4abb-8e69-dbac3d336c2f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1db78f1489815a71dbe223fc2ec4922416178e88
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378931"
---
# <a name="istidevicecontrol-com-interface"></a>IStiDeviceControl COM 接口





**IStiDeviceControl** COM 接口提供[用户模式下仍映像微型驱动程序](overview-of-sti-components.md#ddk-user-mode-still-image-minidrivers-si)有权访问信息存储在[静止图像事件监控程序](overview-of-sti-components.md#ddk-still-image-event-monitor-si)。 它还允许微型驱动程序将信息写入静止图像错误日志。

由定义的方法**IStiDeviceControl**接口包括以下：

<a href="" id="istidevicecontrol--addref"></a>[**IStiDeviceControl::AddRef**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-addref)  
增量**IStiDeviceControl**接口的引用计数。

<a href="" id="istidevicecontrol--getmydeviceopenmode"></a>[**IStiDeviceControl::GetMyDeviceOpenMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-getmydeviceopenmode)  
允许静止图像微型驱动程序以获取应用程序创建的静态图像设备实例时指定的传输模式。

<a href="" id="istidevicecontrol--getmydeviceportname"></a>[**IStiDeviceControl::GetMyDevicePortName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)  
允许静止图像微型驱动程序以获取设备的端口名称。

<a href="" id="istidevicecontrol--release"></a>[**IStiDeviceControl::Release**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-release)  
关闭的实例 COM 对象，定义**IStiDeviceControl**接口，并且对接口中删除访问权限。

<a href="" id="istidevicecontrol--writetoerrorlog"></a>[**IStiDeviceControl::WriteToErrorLog**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-writetoerrorlog)  
允许静止图像微型驱动程序将消息写入到静止图像错误日志。

 

 





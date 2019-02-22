---
title: IStiDeviceControl COM 接口
description: IStiDeviceControl COM 接口
ms.assetid: 6d98f5d7-c471-4abb-8e69-dbac3d336c2f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c6daee1b03f6da3082b9959cb95485d0ea21b18
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555374"
---
# <a name="istidevicecontrol-com-interface"></a>IStiDeviceControl COM 接口





**IStiDeviceControl** COM 接口提供[用户模式下仍映像微型驱动程序](overview-of-sti-components.md#ddk-user-mode-still-image-minidrivers-si)有权访问信息存储在[静止图像事件监控程序](overview-of-sti-components.md#ddk-still-image-event-monitor-si)。 它还允许微型驱动程序将信息写入静止图像错误日志。

由定义的方法**IStiDeviceControl**接口包括以下：

<a href="" id="istidevicecontrol--addref"></a>[**IStiDeviceControl::AddRef**](https://msdn.microsoft.com/library/windows/hardware/ff542933)  
增量**IStiDeviceControl**接口的引用计数。

<a href="" id="istidevicecontrol--getmydeviceopenmode"></a>[**IStiDeviceControl::GetMyDeviceOpenMode**](https://msdn.microsoft.com/library/windows/hardware/ff542942)  
允许静止图像微型驱动程序以获取应用程序创建的静态图像设备实例时指定的传输模式。

<a href="" id="istidevicecontrol--getmydeviceportname"></a>[**IStiDeviceControl::GetMyDevicePortName**](https://msdn.microsoft.com/library/windows/hardware/ff542944)  
允许静止图像微型驱动程序以获取设备的端口名称。

<a href="" id="istidevicecontrol--release"></a>[**IStiDeviceControl::Release**](https://msdn.microsoft.com/library/windows/hardware/ff543725)  
关闭的实例 COM 对象，定义**IStiDeviceControl**接口，并且对接口中删除访问权限。

<a href="" id="istidevicecontrol--writetoerrorlog"></a>[**IStiDeviceControl::WriteToErrorLog**](https://msdn.microsoft.com/library/windows/hardware/ff543727)  
允许静止图像微型驱动程序将消息写入到静止图像错误日志。

 

 





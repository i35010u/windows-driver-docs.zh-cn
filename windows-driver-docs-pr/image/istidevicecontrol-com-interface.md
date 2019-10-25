---
title: IStiDeviceControl COM 接口
description: IStiDeviceControl COM 接口
ms.assetid: 6d98f5d7-c471-4abb-8e69-dbac3d336c2f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 623cef89bce3c950bdbae3fd1cdd2f5379eaebb8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840809"
---
# <a name="istidevicecontrol-com-interface"></a>IStiDeviceControl COM 接口





**IStiDeviceControl** COM 接口为[用户模式静止图像微型驱动程序](overview-of-sti-components.md#ddk-user-mode-still-image-minidrivers-si)提供对存储在[静止图像事件监视器](overview-of-sti-components.md#ddk-still-image-event-monitor-si)中的信息的访问权限。 它还允许微型驱动程序将信息写入仍图像错误日志。

**IStiDeviceControl**接口定义的方法包括：

<a href="" id="istidevicecontrol--addref"></a>[**IStiDeviceControl：： AddRef**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-addref)  
递增**IStiDeviceControl**接口的引用计数。

<a href="" id="istidevicecontrol--getmydeviceopenmode"></a>[**IStiDeviceControl::GetMyDeviceOpenMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceopenmode)  
允许静态图像微型驱动程序获取应用程序在创建静止图像设备实例时指定的传输模式。

<a href="" id="istidevicecontrol--getmydeviceportname"></a>[**IStiDeviceControl::GetMyDevicePortName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)  
允许静态图像微型驱动程序获取设备的端口名称。

<a href="" id="istidevicecontrol--release"></a>[**IStiDeviceControl：： Release**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-release)  
关闭用于定义**IStiDeviceControl**接口的实例 COM 对象，并删除对接口的访问。

<a href="" id="istidevicecontrol--writetoerrorlog"></a>[**IStiDeviceControl::WriteToErrorLog**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-writetoerrorlog)  
允许静态图像微型驱动程序将消息写入静止图像错误日志。

 

 





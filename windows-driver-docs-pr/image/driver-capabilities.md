---
title: 驱动程序功能
description: 驱动程序功能
ms.assetid: 639eff56-655d-4b6a-95f0-daa1daf62fae
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a620a85bc134e87b22c2cb1ffd383e4c9bd33be3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840851"
---
# <a name="driver-capabilities"></a>驱动程序功能





所有 WIA 微型驱动程序都必须定义设备处理通知事件和命令的能力。 本部分介绍这些微型驱动程序功能。

WIA 微型驱动程序负责生成一个表，该表列出了它支持的所有事件和命令。 下图说明了 WIA 微型驱动程序生成的功能表。

![阐释 wia 微型驱动程序功能表的关系图](images/wia-capabilitiestable.png)

功能表定义为[**WIA\_DEV\_CAP\_winspool.drv**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_dev_cap_drv)结构的数组。 当 WIA 服务调用[**IWiaMiniDrv：:D rvgetcapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)方法时，微型驱动程序必须构造此数组，并将其返回到 WIA 服务。

### <a name="defining-supported-events-and-commands"></a>定义支持的事件和命令

WIA 微型驱动程序必须描述设备为 WIA 服务支持的事件和命令。

### <a name="events"></a>事件

*事件*是必须向驱动程序报告的设备级别的操作。 例如，扫描仪可能有一个标记为 "扫描" 的前面板按钮。 当用户按下此按钮时，他们会希望扫描程序开始扫描，或至少在应用程序启动扫描时开始扫描。

WIA 支持两种类型的事件：

<a href="" id="action-event"></a>操作事件  
*操作事件*启动已注册的用于处理此类事件的应用程序。 例如，Microsoft 扫描仪和照相机向导是扫描事件（其他应用程序也可以注册此事件）的已注册处理程序。 当驱动程序发送扫描事件时，WIA 服务将启动扫描仪和照相机向导来处理此事件。 此类事件通常称为*永久性事件*。

<a href="" id="notification-event"></a>通知事件  
*通知事件*只发送到已在运行并已指示 WIA 服务应接收此事件的应用程序。 如果应用程序未运行，则不会启动它来处理此事件。

事件可以是操作事件和通知事件。

### <a name="commands"></a>命令

WIA 设备命令是 WIA 服务（代表图像应用程序）发送到 WIA 微型驱动程序的请求，指示微型驱动程序执行某个操作。 例如，WIA 摄像机微型驱动程序可能处理 "**拍摄照片**" 命令。 此命令指示微型驱动程序对数字照相机设备进行排序以拍摄新图片。

**请注意**   "扫描仪和照相机" 向导会立即响应用户，即使它仍在后台进行清理。 例如，当用户请求取消操作时，"扫描仪和照相机向导" 窗口会立即关闭。但是，扫描仪和照相机向导有一个单独的获取线程，该线程在窗口关闭后将继续运行。 这种单独的线程可以立即响应用户的请求，但允许在不影响用户体验的情况下完成无法中断的必要任务和任务。

 

 

 





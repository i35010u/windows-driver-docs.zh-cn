---
title: 驱动程序功能
description: 驱动程序功能
ms.assetid: 639eff56-655d-4b6a-95f0-daa1daf62fae
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12e7166ebca9173164eef8988ff5e68555b32d96
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519986"
---
# <a name="driver-capabilities"></a>驱动程序功能





所有 WIA 微型驱动程序必须都定义设备的功能来处理通知事件和命令。 本部分介绍这些微型驱动程序功能。

WIA 微型驱动程序负责生成表，其中列出了所有事件和它支持的命令。 下图说明了 WIA 微型驱动程序生成的功能表。

![说明 wia 微型驱动程序功能表的关系图](images/wia-capabilitiestable.png)

数组的形式定义的功能表[ **WIA\_DEV\_CAP\_DRV** ](https://msdn.microsoft.com/library/windows/hardware/ff550233)结构。 微型驱动程序必须构造此数组并将其返回到 WIA 服务时 WIA 服务调用[ **IWiaMiniDrv::drvGetCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff543977)方法。

### <a name="defining-supported-events-and-commands"></a>定义支持事件和命令

WIA 微型驱动程序必须描述的事件和设备支持到 WIA 服务的命令。

### <a name="events"></a>事件

*事件*是在必须向驱动程序报告的设备级别的操作。 例如，扫描程序可能被标记为"扫描"的前面板按钮。 用户按下此按钮时，他们期望扫描程序以开始扫描，或最起码，应用程序将启动以启动扫描。

WIA 支持两种类型的事件：

<a href="" id="action-event"></a>操作事件  
*操作事件*启动注册用于处理此类事件的应用程序。 例如，Microsoft 扫描仪和照相机向导是扫描事件的已注册处理程序 （此事件也可以注册其他应用程序）。 驱动程序将发送扫描事件，WIA 服务将启动扫描仪和照相机向导来处理此事件。 此类型的事件通常称为*永久性事件*。

<a href="" id="notification-event"></a>通知事件  
一个*通知事件*只被发送到应用程序已运行且具有指定给 WIA 服务他们应该接收此事件。 如果未运行该应用程序，它不被开始处理此事件。

事件可以是操作事件和通知事件。

### <a name="commands"></a>命令

WIA 设备命令是 WIA 微型驱动程序，可指示微型驱动程序来执行某些操作 （代表图像处理应用程序） 将 WIA 服务发送的请求。 例如，可能会处理 WIA 照相机微型驱动程序**拍照**命令。 此命令指示微型驱动程序进行排序数字照相机设备拍摄新图片。

**请注意**  扫描仪和照相机向导立即向用户提供响应，即使它仍具有清理在后台执行。 例如，扫描仪和照相机向导窗口中关闭立即当用户请求取消操作;但是，扫描仪和照相机向导具有单独获取线程继续运行后关闭窗口。 此单独的线程启用即时响应用户的请求，但允许必要的任务和不能中断不会影响用户体验的情况下完成的任务。

 

 

 





---
title: STI 组件概述
description: STI 组件概述
ms.assetid: 30aaa622-fb86-42dc-a417-df61e0093db3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbe34f780fcf3f153551987db0b1a21f91ca7a54
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392647"
---
# <a name="overview-of-sti-components"></a>STI 组件概述





下图说明了构成 Microsoft STI 的软件组件。 以下关系图是一个组件列表。

![说明 microsoft sti 组件的关系图](images/sticomp.png)

### <a href="" id="ddk-imaging-application-si"></a>图像处理应用程序

图像处理应用程序通常接收、 显示和允许捕获静止图像编辑。 通过调用图像收购 API，如 TWAIN，他们获得的映像。 它们必须自行注册静止图像事件监视器，与通过[IStillImage COM 接口](istillimage-com-interface.md)。 有关详细信息，请参阅[创建推送模型意识的应用程序](creating-push-model-aware-applications.md)。

### <a href="" id="ddk-image-acquisition-api-si"></a>图像采集 API

TWAIN，ISIS 和 Adobe Systems Acquire 是图像采集 Api 的示例。 下图说明了 TWAIN。 供应商提供了 TWAIN 数据源是与仍映像设备进行通信的特定于设备的、 特定于操作系统的组件。

在 Microsoft STI 下 TWAIN 数据源调用方法提供[IStillImage](istillimage-com-interface.md)并[IStiDevice](istidevice-com-interface.md)接口。 有关详细信息，请参阅[图像采集 api 创建特定于设备的组件](creating-device-specific-components-for-image-acquisition-apis.md)。

### <a href="" id="ddk-scanners-and-cameras-control-panel-si"></a>扫描仪和照相机控件面板

扫描仪和照相机控件面板使用户能够执行以下操作：

-   查看已安装的静止图像设备的列表。

-   测试仍映像的设备。

-   查看和修改提供的信息由供应商提供特定于设备的[的属性表页静止图像设备](property-sheet-pages-for-still-image-devices.md)。

-   将分配[静止图像的设备事件](still-image-device-events.md)给特定应用程序。

### <a href="" id="ddk-still-image-event-monitor-si"></a>静止图像事件监视器

静止图像事件监视器驻留在静止图像服务器进程中。 它维护一个数据库的所有静止图像设备 （即插即用和 Play−compatible 设备和那些通过添加硬件向导安装）。 它还维护已注册的应用程序和仍映像设备事件的数据库。

事件监视器等待仍映像设备事件。 （对于不会生成仍映像设备事件的较旧驱动程序支持的设备，事件监视器创建一个轮询线程。）检测到事件时，事件监视器启动的应用程序的用户以前已 （通过扫描仪和照相机控件面板） 分配给该事件。 如果用户已分配给多个应用程序的事件，事件监视器，询问用户要启动的应用程序。 如果该事件尚未分配到任何应用程序，则忽略它。

有关静止图像事件监视器的详细信息，请参阅*静止图像*Microsoft Windows SDK 文档中。

### <a href="" id="ddk-com-interfaces-for-still-image-si"></a>静态图像的 COM 接口

Microsoft STI 定义一组 COM 接口，提供的各种 Microsoft STI 组件之间的通信路径。 定义以下 COM 接口：

[IStillImage COM 接口](istillimage-com-interface.md)

[IStiDevice COM 接口](istidevice-com-interface.md)

[IStiUSD COM 接口](istiusd-com-interface.md)

[IStiDeviceControl COM 接口](istidevicecontrol-com-interface.md)

### <a href="" id="ddk-user-mode-still-image-minidrivers-si"></a>用户模式下仍映像微型驱动程序

用户模式下仍映像微型驱动程序是为提供适当的内核模式驱动程序的特定于设备的用户模式接口的供应商提供的组件。 每个这些用户模式驱动程序必须实现[IStiUSD COM 接口](istiusd-com-interface.md)。 它们与内核模式驱动程序通信通过调用[ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)， **ReadFile**， **WriteFile**，和[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216) Win32 函数 （Microsoft Windows SDK 文档中所述）。 有关详细信息，请参阅[创建用户模式下仍映像微型驱动程序](creating-a-user-mode-still-image-minidriver.md)。

### <a href="" id="ddk-kernel-mode-still-image-drivers-si"></a>内核模式下仍映像驱动程序

内核模式下仍映像驱动程序打包为传递到静态图像设备连接到特定的总线类型的数据。 Microsoft 提供了基于 WDM 的内核模式下仍映像驱动程序对于 USB 和 SCSI 总线。 有关详细信息，请参阅[访问内核模式设备驱动程序仍映像](accessing-kernel-mode-drivers-for-still-image-devices.md)。

对于仍连接到其他总线映像设备，用户模式下微型驱动程序进行通信与内核模式总线驱动程序堆栈直接。

供应商只需提供内核模式下仍映像驱动程序，如果设备不符合 Microsoft 提供的驱动程序。

### <a href="" id="ddk-kernel-mode-bus-driver-stacks-si"></a>内核模式总线驱动程序堆栈

Microsoft 仍支持图像设备连接到 SCSI、 USB、 并行，IEEE 1394 兼容和串行总线，以及设备连接到如红外接口，如下所示：

<a href="" id="devices-connected-to-scsi-and-usb-buses"></a>**设备连接到 SCSI 和 USB 总线**  
用户模式驱动程序调用总线特有[内核模式驱动程序进行静止图像设备](accessing-kernel-mode-drivers-for-still-image-devices.md)。

<a href="" id="devices-connected-to-a-parallel-port"></a>**连接到并行端口设备**  
扩展功能端口 (ECP) 并支持增强的并行端口 (EPP) 模式。 供应商提供内核模式*筛选器驱动程序*可以添加用户模式下仍映像驱动程序和内核模式总线驱动程序堆栈之间。 (有关并行端口驱动程序的详细信息，请参阅[并行设备设计指南](https://msdn.microsoft.com/library/windows/hardware/ff544263)并[并行设备引用](https://msdn.microsoft.com/library/windows/hardware/ff544269)。 有关筛选器驱动程序的详细信息，请参阅[筛选器驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff545890)。)

<a href="" id="devices-connected-to-an-ieee-1394-bus"></a>**设备连接到 IEEE 1394 总线**  
对于支持 sbp-2 协议的设备，用户模式驱动程序可以调用的 sbp-2 接口。 否则，供应商提供的筛选器驱动程序是必需的。

<a href="" id="devices-connected-to-a-serial-port"></a>**设备连接到串行端口**  
使用标准的串行端口驱动程序。 (有关详细信息，请参阅[串行设备和驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff547451)。)

<a href="" id="devices-connected-to-an-infrared-interface"></a>**设备连接到红外接口**  
驱动程序可以调用**IrSock**软件界面 （Microsoft Windows SDK 文档中所述）。

供应商只需为 Microsoft 驱动程序不支持的总线提供总线驱动程序。

 

 





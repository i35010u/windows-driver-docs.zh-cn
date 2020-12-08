---
title: STI 组件概述
description: STI 组件概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27fc0246e2a331538d31160805c30d63f44bcdab
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841097"
---
# <a name="overview-of-sti-components"></a>STI 组件概述





下图说明了构成 Microsoft STI 的软件组件。 下面的关系图是一个组件列表。

![说明 microsoft sti 组件的示意图](images/sticomp.png)

### <a name="imaging-application"></a><a href="" id="ddk-imaging-application-si"></a>图像处理应用程序

图像处理应用程序通常会接收、显示和允许编辑捕获的静止图像。 它们通过调用图像获取 API （如 TWAIN）来获取映像。 它们必须通过 [ISTILLIMAGE COM 接口](istillimage-com-interface.md)向其自身注册静止图像事件监视器。 有关详细信息，请参阅 [创建 Push-Model 感知的应用程序](creating-push-model-aware-applications.md)。

### <a name="image-acquisition-api"></a><a href="" id="ddk-image-acquisition-api-si"></a>映像获取 API

"TWAIN"、"ISIS" 和 "Adobe Systems" 获取图像获取 Api 的示例。 此图说明了 TWAIN。 供应商提供的 TWAIN 数据源是设备特定的、特定于操作系统的组件，这些组件与静态图像设备通信。

在 Microsoft STI 下，TWAIN 数据源调用 [IStillImage](istillimage-com-interface.md)和 [IStiDevice](istidevice-com-interface.md) 接口提供的方法。 有关详细信息，请参阅 [创建映像获取 api Device-Specific 组件](creating-device-specific-components-for-image-acquisition-apis.md)。

### <a name="scanners-and-cameras-control-panel"></a><a href="" id="ddk-scanners-and-cameras-control-panel-si"></a>扫描仪和照相机控制面板

"扫描仪和照相机" 控制面板使用户能够执行以下操作：

-   查看已安装的静止图像设备的列表。

-   测试静止图像设备。

-   查看和修改供应商提供的、特定于设备的 [属性表页的静止图像设备](property-sheet-pages-for-still-image-devices.md)的信息。

-   将 [静止图像设备事件](still-image-device-events.md) 分配给特定的应用程序。

### <a name="still-image-event-monitor"></a><a href="" id="ddk-still-image-event-monitor-si"></a>静止图像事件监视器

静止图像事件监视器驻留在静止图像服务器进程中。 它在即插即用−兼容设备和通过添加硬件向导) 安装的设备 (维护所有静止图像设备的数据库。 它还维护已注册应用程序的数据库和仍为映像的设备事件。

事件监视器等待仍图像设备事件。  (对于不生成静止图像设备事件的旧驱动程序所支持的设备，事件监视器会创建轮询线程。 ) 检测到事件时，事件监视器会通过 "扫描仪和相机" 控制面板) 启动用户以前分配给该 (事件的应用程序。 如果用户已将事件分配给多个应用程序，则事件监视器会要求用户启动哪个应用程序。 如果事件尚未分配到任何应用程序，则将其忽略。

有关静止图像事件监视器的详细信息，请参阅 Microsoft Windows SDK 文档中的 *静止图像* 。

### <a name="com-interfaces-for-still-image"></a><a href="" id="ddk-com-interfaces-for-still-image-si"></a>静态图像的 COM 接口

Microsoft STI 定义一组 COM 接口，这些接口提供各种 Microsoft STI 组件之间的通信路径。 定义了下列 COM 接口：

[IStillImage COM 接口](istillimage-com-interface.md)

[IStiDevice COM 接口](istidevice-com-interface.md)

[IStiUSD COM 接口](istiusd-com-interface.md)

[IStiDeviceControl COM 接口](istidevicecontrol-com-interface.md)

### <a name="user-mode-still-image-minidrivers"></a><a href="" id="ddk-user-mode-still-image-minidrivers-si"></a>用户模式静止图像微型驱动程序

用户模式静止图像微型驱动程序是供应商提供的组件，可向相应的内核模式驱动程序提供设备特定的用户模式接口。 其中每个用户模式驱动程序必须实现 [ISTIUSD COM 接口](istiusd-com-interface.md)。 它们通过调用 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea)、 **ReadFile**、 **WriteFile** 和 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) Win32 函数与内核模式驱动程序通信， () 的 Microsoft Windows SDK 文档中所述。 有关详细信息，请参阅 [创建 User-Mode 静止图像微型驱动程序](creating-a-user-mode-still-image-minidriver.md)。

### <a name="kernel-mode-still-image-drivers"></a><a href="" id="ddk-kernel-mode-still-image-drivers-si"></a>内核模式静止映像驱动程序

内核模式静止映像驱动程序包数据，用于传递到连接到特定总线类型的静止图像设备。 Microsoft 为 USB 和 SCSI 总线提供基于 WDM 的内核模式静止映像驱动程序。 有关详细信息，请参阅 [访问静止图像设备 Kernel-Mode 驱动程序](accessing-kernel-mode-drivers-for-still-image-devices.md)。

对于连接到其他总线的静止图像设备，用户模式微型驱动程序直接与内核模式总线驱动程序堆栈进行通信。

如果设备与 Microsoft 提供的驱动程序不兼容，则供应商只需提供内核模式的静止映像驱动程序。

### <a name="kernel-mode-bus-driver-stacks"></a><a href="" id="ddk-kernel-mode-bus-driver-stacks-si"></a>内核模式总线驱动程序堆栈

Microsoft 支持连接到 SCSI、USB、并行、IEEE 1394 兼容的设备和串行总线的静止图像设备，以及连接到红外接口的设备，如下所示：

<a href="" id="devices-connected-to-scsi-and-usb-buses"></a>**连接到 SCSI 总线和 USB 总线的设备**  
用户模式驱动程序为静止图像设备调用特定于总线的 [内核模式驱动程序](accessing-kernel-mode-drivers-for-still-image-devices.md)。

<a href="" id="devices-connected-to-a-parallel-port"></a>**连接到并行端口的设备**  
支持 (ECP) 和增强型并行端口 (EPP) 模式的扩展功能端口。 供应商提供的内核模式 *筛选器驱动程序* 可以添加到用户模式静止映像驱动程序和内核模式总线驱动程序堆栈之间。  (有关并行端口驱动程序的详细信息，请参阅 [并行设备设计指南](/previous-versions/ff544263(v=vs.85)) 和 [并行设备参考](/windows-hardware/drivers/ddi/index)。 有关筛选器驱动程序的详细信息，请参阅 [筛选器驱动程序](../kernel/filter-drivers.md)。 ) 

<a href="" id="devices-connected-to-an-ieee-1394-bus"></a>**连接到 IEEE 1394 总线的设备**  
对于支持 SBP 协议的设备，用户模式驱动程序可以调用 Microsoft 的 SBP 接口。 否则，需要供应商提供的筛选器驱动程序。

<a href="" id="devices-connected-to-a-serial-port"></a>**连接到串行端口的设备**  
使用标准串行端口驱动程序。  (有关详细信息，请参阅 [串行设备和驱动程序](../serports/using-serial-sys-and-serenum-sys.md)。 ) 

<a href="" id="devices-connected-to-an-infrared-interface"></a>**连接到红外线接口的设备**  
驱动程序可以调用 **IrSock** software 接口 (Microsoft Windows SDK 文档) 中所述。

供应商只需要为 Microsoft 驱动程序不支持的总线提供总线驱动程序。


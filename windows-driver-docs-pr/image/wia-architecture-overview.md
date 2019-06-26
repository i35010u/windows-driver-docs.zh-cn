---
title: WIA 体系结构概述
description: WIA 体系结构概述
ms.assetid: 47f44042-f22b-4ee0-88c5-fc977bf13791
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 86b0d7f282e233c07bc1b7944f114e59eeabdacf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375363"
---
# <a name="wia-architecture-overview"></a>WIA 体系结构概述

WIA 作为组件对象模型 (COM) 扩展进程服务器，以确保客户端应用程序的可靠的操作。 

WIA 有三个主要组件： WIA 服务、 WIA 驱动程序服务库和供应商用户模式驱动程序。

-   WIA 服务枚举成像设备、 检索设备属性、 设置事件的设备，并创建设备对象。

-   WIA 驱动程序服务库实现独立于设备的所有服务。

-   供应商用户模式驱动程序将 WIA 属性和命令映射到特定设备。 有两种类型的 WIA 供应商用户模式驱动程序：

    -   微型驱动程序：这是最常见的供应商驱动程序类型。 它是实现 WIA 微型驱动程序接口的 COM 对象。 供应商可以充分利用所有 WIA 功能和使用此类型的驱动程序的功能。
    
    -   Microdriver:此驱动程序是更多的限制比微型驱动程序，因此，开发更简单。 它主要用于基本扫描程序的设备。 此驱动程序不是 COM 对象;它是导出几个函数的 DLL。 Microdrivers 不能用于相机的设备。

下图说明了 WIA 体系结构。

![说明 wia 组件的关系图](images/art-1.png)

### <a name="imaging-applications"></a>图像处理应用程序

图像处理应用程序不能直接与微型驱动程序，但与 WIA 服务通过 WIA 应用程序编程接口 (API) 来访问图像，并获得 WIA 的设备中的数据通信。 一个常见的系统提供用户界面或供应商提供的用户界面，可以使用这些应用程序。 有关图像处理应用程序 WIA API 的详细信息，请参阅 Microsoft Windows SDK 文档。

### <a name="wia-service"></a>WIA 服务

WIA 服务是与图像处理应用程序和 WIA 微型驱动程序进行通信的系统提供的组件。 在另一个进程中的应用程序和与 WIA 微型驱动程序相同的进程执行 WIA 服务。 应用程序及其设备将请求定向到 WIA 服务，又将请求定向到相应的微型驱动程序通过 WIA 的设备驱动程序接口 (DDI)。

### <a name="wia-driver-services-library"></a>WIA 驱动程序服务库

WIA 驱动程序服务库是为 WIA 微型驱动程序提供帮助器函数的系统提供的组件。 微型驱动程序可以调用帮助程序函数来执行以下任务：

-   初始化 WIA 驱动程序项树。

-   读取、 写入和验证设备属性。

-   将数据传输。

或者，微型驱动程序可以执行此类任务本身。 通过利用帮助器函数，可以同时仍可以灵活地开发单个解决方案减少开发时间和 WIA 微型驱动程序的大小。

### <a name="wia-user-mode-minidrivers"></a>WIA 用户模式微型驱动程序

WIA 微型驱动程序将供应商提供，将 WIA 属性更改和命令指向图像处理设备的用户模式组件。 微型驱动程序实现 WIA DDI 称为 WIA 服务与微型驱动程序进行通信。

WIA 微型驱动程序实现的标准 WIA 微型驱动程序接口。 微型驱动程序与标准的 Microsoft Windows 内核模式驱动程序，如 USB 驱动程序通过成像设备进行通信。 微型驱动程序与内核模式驱动程序通过调用[ **CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)， **ReadFile**， **WriteFile**，和**DeviceIoControl** Win32 函数 （Microsoft Windows SDK 文档中所述）。

图像处理应用程序不能进行直接调用到 WIA 微型驱动程序。 只有 WIA 服务允许直接调用该驱动程序。

### <a name="kernel-io-drivers"></a>内核 I/O 驱动程序

内核模式下仍映像驱动程序是系统提供的或 IHV 提供组件，将数据传递到或从静态图像设备。 内核模式下仍映像驱动程序是特定于总线的。

Microsoft 提供了基于 WDM 的内核模式静止图像对于 USB、 SCSI、 和 IEEE 1394 总线驱动程序。 请参阅[访问内核模式设备驱动程序仍映像](accessing-kernel-mode-drivers-for-still-image-devices.md)有关详细信息。

供应商必须提供内核模式下仍映像驱动程序*仅*其映像的设备是否与 Microsoft 提供的内核模式不兼容 I/O 驱动程序。

 

---
title: WIA 体系结构概述
description: WIA 体系结构概述
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: ae7cb287283bff5382f9bdfc0fd6deee6f03b6ab
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816713"
---
# <a name="wia-architecture-overview"></a>WIA 体系结构概述

WIA 作为组件对象模型实现 (COM) 进程外服务器，确保客户端应用程序的强大操作。 

WIA 包含三个主要组件： WIA 服务、WIA 驱动程序服务库和供应商用户模式驱动程序。

-   WIA 服务枚举映像设备、检索设备属性、设置设备事件，并创建设备对象。

-   WIA 驱动程序服务库实现与设备无关的所有服务。

-   供应商用户模式驱动程序将 WIA 属性和命令映射到特定设备。 WIA 供应商用户模式驱动程序有两种类型：

    -   微型驱动程序：这是最常见的供应商驱动程序类型。 它是实现 WIA 微型驱动程序接口的 COM 对象。 供应商可以利用此类驱动程序的所有 WIA 功能和功能。
    
    -   Microdriver：此驱动程序比微型驱动程序更受限制，因此更易于开发。 它主要用于基本扫描设备。 此驱动程序不是 COM 对象;它是导出一些函数的 DLL。 照相机设备不能使用 Microdrivers。

下图说明了 WIA 体系结构。

![阐释 wia 组件的关系图](images/art-1.png)

### <a name="imaging-applications"></a>图像应用程序

图像处理应用程序不直接与微型驱动程序通信，而是通过 WIA 应用程序编程接口 (API) 与 WIA 服务通信，以便从 WIA 设备访问图像和获取数据。 这些应用程序可以使用系统提供的通用用户界面或供应商提供的用户界面。 有关用于映像应用程序的 WIA API 的详细信息，请参阅 Microsoft Windows SDK 文档。

### <a name="wia-service"></a>WIA 服务

WIA 服务是系统提供的组件，可与图像处理应用程序和 WIA 微型驱动程序进行通信。 WIA 服务在独立于应用程序的进程中执行，并在与 WIA 微型驱动程序相同的进程中执行。 应用程序将其设备请求定向到 WIA 服务，后者会通过 WIA 设备驱动程序接口 (DDI) 将请求定向到相应的微型驱动程序。

### <a name="wia-driver-services-library"></a>WIA 驱动程序服务库

WIA 驱动程序服务库是系统提供的组件，它为 WIA 微型驱动程序提供 helper 函数。 微型驱动程序可以调用 helper 函数来执行如下任务：

-   初始化 WIA 驱动程序项树。

-   读取、写入和验证设备属性。

-   传输数据。

或者，微型驱动程序可以执行此类任务本身。 利用帮助程序函数，你可以减少开发时间和 WIA 微型驱动程序的大小，同时仍然可以灵活地开发单个解决方案。

### <a name="wia-user-mode-minidrivers"></a>WIA User-Mode 微型驱动程序

WIA 微型驱动程序是由供应商提供的用户模式组件，可将 WIA 属性更改和命令定向到图像设备。 微型驱动程序实现 WIA DDI，WIA 服务调用它来与微型驱动程序进行通信。

WIA 微型驱动程序实现了标准的 WIA 微型驱动程序接口。 微型驱动程序通过标准 Microsoft Windows 内核模式驱动程序（如 USB 驱动程序）与图像设备进行通信。 微型驱动程序通过调用 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea)、 **ReadFile**、 **WriteFile** 和 **DeviceIoControl** Win32 函数与内核模式驱动程序通信， (Microsoft Windows SDK 文档) 中所述。

图像应用程序无法直接调用 WIA 微型驱动程序。 仅允许 WIA 服务直接调用该驱动程序。

### <a name="kernel-io-drivers"></a>内核 i/o 驱动程序

内核模式的静止映像驱动程序是系统提供的或由 IHV 提供的组件，可向静止图像设备发送数据。 内核模式的静止映像驱动程序是特定于总线的。

Microsoft 为 USB、SCSI 和 IEEE 1394 总线提供基于 WDM 的内核模式静止映像驱动程序。 有关详细信息，请参阅 [访问静止图像设备 Kernel-Mode 驱动程序](accessing-kernel-mode-drivers-for-still-image-devices.md) 。

仅当供应商的图像处理设备与 Microsoft 提供的内核模式 i/o 驱动程序不兼容时，供应商 *才* 必须提供该驱动程序的内核模式。


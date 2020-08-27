---
description: Windows 便携设备的体系结构概述
title: 体系结构概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c1195f115d11024cde9ab73c94d2af4e02b9964
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969565"
---
# <a name="architecture-overview"></a>体系结构概述


WPD 体系结构可以分为三个过程。 在这些过程中，是 WPD 的三个主要组件： API、序列化程序和驱动程序。 下图描绘了构成 WPD 体系结构的这些过程和组件。

![3个进程构成 wpd](images/wpd_overview_figure1.png)

## <a name="span-idthe_wpd_application_programming_interfacespanspan-idthe_wpd_application_programming_interfacespanspan-idthe_wpd_application_programming_interfacespanthe-wpd-application-programming-interface"></a><span id="The_WPD_Application_Programming_Interface"></span><span id="the_wpd_application_programming_interface"></span><span id="THE_WPD_APPLICATION_PROGRAMMING_INTERFACE"></span>WPD 应用程序编程接口


WPD API 作为进程内 COM 服务器实现。 API 使用标准的 Microsoft Win32 Api 与相应的 WPD 驱动程序通信。 API 对象和驱动程序使用称为 WPD 序列化程序的组件将参数打包或解压缩到 Windows 驱动程序框架， (WDF) 用户模式驱动程序框架 (UMDF) 缓冲区。

## <a name="span-idthe_wpd_serializerspanspan-idthe_wpd_serializerspanspan-idthe_wpd_serializerspanthe-wpd-serializer"></a><span id="The_WPD_Serializer"></span><span id="the_wpd_serializer"></span><span id="THE_WPD_SERIALIZER"></span>WPD 序列化程序


WPD 序列化程序还实现为进程内 COM 服务器。 WPD API 使用序列化程序将命令和参数打包到发送到驱动程序的消息缓冲区。 驱动程序使用序列化程序来解包这些消息缓冲区以便进行处理。 驱动程序还使用序列化程序将数据和参数打包到返回到 WPD API 的响应缓冲区，而 WPD API 使用序列化程序将这些响应缓冲区解包，以将结果返回给调用方。

## <a name="span-idwpd_driverspanspan-idwpd_driverspanspan-idwpd_driverspanwpd-driver"></a><span id="WPD_Driver"></span><span id="wpd_driver"></span><span id="WPD_DRIVER"></span>WPD 驱动程序


WPD 驱动程序作为标准 Windows 驱动程序框架实现， (WDF) 用户模式驱动程序框架 (UMDF) 驱动程序。 WPD 驱动程序由 WUDF 在单独的进程中托管，称为驱动程序主机。

驱动程序接收来自 WUDF 反射器的消息 (这不会显示在关系图中，因为接收缓冲区对驱动程序并不重要。 ) 的详细信息，请参阅 WUDF 文档。 该驱动程序实现了 WPD 特定的 IOCTL 处理程序，用于处理 WPD API 接收到的 WPD 消息。 驱动程序使用 WPD 序列化程序将命令和参数解压缩到这些消息缓冲区，并将响应打包到缓冲区中。

WPD 驱动程序可以通过使用内核模式驱动程序与其设备通信，通常通过 Win32 文件 (操作访问，例如 CreateFile、ReadFile、WriteFile 等) 。 对于常见的总线，Microsoft 将为供应商提供要使用的标准内核驱动程序，这将允许供应商交付仅限用户模式的驱动程序解决方案。

 

 





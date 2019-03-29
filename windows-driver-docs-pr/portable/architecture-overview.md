---
Description: Architecture overview of Windows portable devices
title: 体系结构概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c788eed2e620d9c9e940d718f1fa09d78a06d3ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563968"
---
# <a name="architecture-overview"></a>体系结构概述


WPD 体系结构可以分为三个进程。 在这些进程内是 WPD 的三个主要组件： 的 API、 序列化程序和驱动程序。 下图描绘了这些流程和构成 WPD 体系结构的组件。

![构成 wpd 3 个进程](images/wpd_overview_figure1.png)

## <a name="span-idthewpdapplicationprogramminginterfacespanspan-idthewpdapplicationprogramminginterfacespanspan-idthewpdapplicationprogramminginterfacespanthe-wpd-application-programming-interface"></a><span id="The_WPD_Application_Programming_Interface"></span><span id="the_wpd_application_programming_interface"></span><span id="THE_WPD_APPLICATION_PROGRAMMING_INTERFACE"></span>WPD 应用程序编程接口


WPD API 作为进程内 COM 服务器实现。 API 使用标准 Microsoft Win32 Api 来与相应的 WPD 驱动程序进行通信。 通过 API 对象和驱动程序使用名为 WPD 序列化程序的组件打包或解包到或从 Windows 驱动程序框架 (WDF)-用户-模式驱动程序框架 (UMDF) 缓冲区参数。

## <a name="span-idthewpdserializerspanspan-idthewpdserializerspanspan-idthewpdserializerspanthe-wpd-serializer"></a><span id="The_WPD_Serializer"></span><span id="the_wpd_serializer"></span><span id="THE_WPD_SERIALIZER"></span>WPD 序列化程序


WPD 序列化程序也作为进程内 COM 服务器实现。 WPD API 使用序列化程序打包到消息缓冲区发送到该驱动程序的命令和参数。 驱动程序使用序列化程序进行解包处理这些消息缓冲区。 驱动程序还使用序列化程序打包到响应缓冲区 WPD api 返回的数据和参数和 WPD API 使用序列化程序进行解包这些响应缓冲区以将结果返回到调用方。

## <a name="span-idwpddriverspanspan-idwpddriverspanspan-idwpddriverspanwpd-driver"></a><span id="WPD_Driver"></span><span id="wpd_driver"></span><span id="WPD_DRIVER"></span>WPD 驱动程序


WPD 驱动程序作为标准的 Windows 驱动程序框架 (WDF)-用户-模式驱动程序框架 (UMDF) 驱动程序实现。 WPD 驱动程序由 WUDF 托管在单独的进程中被称为驱动程序主机。

该驱动程序接收消息从 WUDF 反射器 （这未显示在图中，因为接收缓冲区的方式并不重要的驱动程序。 请参阅 WUDF 文档的详细信息）。 该驱动程序实现特定于的 WPD IOCTL 处理程序来处理由 WPD API 接收的 WPD 消息。 若要解压缩命令和参数从这些消息缓冲区，然后打包到缓冲区的响应，则驱动程序使用 WPD 序列化程序。

WPD 驱动程序可能会进行通信时使用他们的设备通过内核模式驱动程序，通常通过 Win32 文件操作 （如 CreateFile、 ReadFile、 WriteFile 等） 访问。 对于常见的总线，Microsoft 将提供标准内核驱动程序供应商可以使用，这将允许供应商提供仅用户模式驱动程序解决方案。

 

 





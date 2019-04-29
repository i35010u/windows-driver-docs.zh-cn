---
title: 后台处理程序组件简介
description: 后台处理程序组件简介
ms.assetid: 4eb6e84a-f75f-4ec2-af4f-0007678d120b
keywords:
- 后台处理程序组件图 WDK 打印
- 打印后台处理程序组件图 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2d5595061d401fcfb4b4e58b510ceee4dc12940
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382613"
---
# <a name="introduction-to-spooler-components"></a>后台处理程序组件简介





在下图说明了 Microsoft Windows 2000 和更高版本的打印后台处理程序的主要组件。

![说明 windows 2000 和更高版本打印后台处理程序的主要组件的关系图](images/spoocomp.png)

<a href="" id="application-"></a>**Application**   
打印应用程序通过调用 GDI 函数创建打印作业。

<a href="" id="gdi-"></a>**GDI**   
图形设备接口 (*GDI*) 包括用户模式和内核模式组件。 用户模式组件，Microsoft Win32 GDI，可供需要图形支持的 Win32 应用程序。 内核模式组件*图形引擎*（或图形呈现引擎），将导出的服务和图形设备驱动程序可以使用的函数。

<a href="" id="winspool-drv-"></a>**Winspool.drv**   
Winspool.drv 是到后台处理程序的客户端接口。 它将导出的函数，构成后台处理程序的 Win32 API，并提供用于访问服务器的 RPC 存根 （stub）。 （GDI 是主要的客户端，但应用程序还调用其 Win32 函数。）

<a href="" id="spoolsv-exe-"></a>**Spoolsv.exe**   
Spoolsv.exe 是后台处理程序的 API 服务器。 它作为操作系统启动时启动的 Windows 2000 （或更高版本） 服务实现。 此模块将为 RPC 接口导出到后台处理程序的 Win32 API 的服务器端。 Spoolsv.exe 的客户端包括 Winspool.drv （本地） 和 Win32spl.dll （远程）。 此模块实现某些 API 函数，但大多数函数调用中传递给[打印提供程序](print-providers.md)通过路由器 (Spoolss.dll)。

<a href="" id="router-"></a>**路由器**   
路由器 Spoolss.dll，确定要调用的打印提供程序基于打印机名称或提供与每个函数调用，句柄，并将传递到正确的提供程序的函数调用。

<a href="" id="print-provider-"></a>**打印提供程序**   
支持指定的打印设备打印提供程序。

<a href="" id="print-monitor-"></a>**打印监视器**   
Windows XP 支持两种类型的打印监视器： 语言监视器和端口监视器。

如果系统正在运行应用程序的本地打印机硬件，"客户端"和"server"是相同的系统 （尽管这不是很明显在关系图中）。

在用户模式下执行后台处理程序的所有组件。

 

 





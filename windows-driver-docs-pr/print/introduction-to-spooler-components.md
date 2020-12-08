---
title: 后台处理程序组件简介
description: 后台处理程序组件简介
keywords:
- 后台处理程序组件图 WDK 打印
- 打印后台处理程序组件图 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01b8dc99c190057677752ec70eab2dbf91639dc3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796663"
---
# <a name="introduction-to-spooler-components"></a>后台处理程序组件简介





下图演示了 Microsoft Windows 2000 和更高版本打印后台处理程序的主要组件。

![说明 windows 2000 和更高版本打印后台处理程序的主要组件的关系图](images/spoocomp.png)

<a href="" id="application-"></a>**程序**   
打印应用程序通过调用 GDI 函数创建打印作业。

<a href="" id="gdi-"></a>**GDI**   
图形设备接口 (*GDI*) 包括用户模式和内核模式组件。 用户模式组件 Microsoft Win32 GDI 由需要图形支持的 Win32 应用程序使用。 *图形引擎* (或图形渲染引擎) 的内核模式组件可导出图形设备驱动程序可以使用的服务和功能。

<a href="" id="winspool-drv-"></a>**Winspool.drv. winspool.drv**   
Winspool.drv. winspool.drv 是后台处理程序的客户端接口。 它将组成后台处理程序的 Win32 API 的函数导出，并为访问服务器提供 RPC 存根。  (GDI 是主客户端，但应用程序也会调用其某些 Win32 函数。 ) 

<a href="" id="spoolsv-exe-"></a>**Spoolsv.exe**   
Spoolsv.exe 是后台处理程序的 API 服务器。 它作为 Windows 2000 (或更高版本) 服务实现，该服务在操作系统启动时启动。 此模块将 RPC 接口导出到后台处理程序的 Win32 API 的服务器端。 Spoolsv.exe 的客户端在本地) 和 Win32spl.dll (远程)  (的客户端。 此模块实现某些 API 函数，但大多数函数调用通过路由器 ( # A0) 传递给 [打印提供程序](print-providers.md) 。

<a href="" id="router-"></a>**路由器**   
路由器 Spoolss.dll 根据每个函数调用中提供的打印机名称或句柄来确定要调用的打印提供程序，并将函数调用传递给正确的提供程序。

<a href="" id="print-provider-"></a>**打印提供程序**   
支持指定打印设备的打印提供程序。

<a href="" id="print-monitor-"></a>**打印监视器**   
Windows XP 支持两种类型的打印监视器：语言监视器和端口监视器。

如果打印机硬件在运行应用程序的系统上是本地的，则 "客户端" 和 "服务器" 是相同的系统 (虽然这在关系图) 中不明显。

所有后台处理程序组件都在用户模式下执行。

 

 





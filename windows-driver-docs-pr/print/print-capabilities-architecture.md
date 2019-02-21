---
title: 打印功能体系结构
description: 打印功能体系结构
ms.assetid: d19438ca-8c88-4835-8445-2799387e0912
keywords:
- 打印功能 WDK，体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9102e16108f775a56d438b3be2aea97396d2be7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542239"
---
# <a name="print-capabilities-architecture"></a>打印功能体系结构


PrintCapabilities 对象返回的[ **IPrintTicketProvider::GetPrintCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff554365)打印驱动程序实现的方法[IPrintTicketProvider 接口](https://msdn.microsoft.com/library/windows/hardware/ff554375). XPSDrv 打印驱动程序必须实现 IPrintTicketProvider 接口除了[ **DrvDeviceCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff548539)函数。

您可以修改较旧的、 基于 GDI 的打印驱动程序提供直接是 PrintCapabilities 文档，而这种修改不是必需。 Windows Vista 打印子系统创建一个 XML PrintCapabilities 文档以便基于 GDI 的驱动程序的不会添加一个返回的功能。 但是，Windows Vista 打印子系统创建 PrintCapabilities 文档包括仅有限的一组参数的 Microsoft Win32 函数**DeviceCapabilities** ，支持。 基于 GDI 的打印驱动程序提供的打印机的特性和功能的完整列表，它必须包括对支持[IPrintTicketProvider 接口](https://msdn.microsoft.com/library/windows/hardware/ff554375)。

下面的列表和关系图说明了不同类型的打印驱动程序如何支持打印功能技术：

<a href="" id="unidrv-or-pscript5-print-driver"></a>Unidrv 或 PScript5 打印驱动程序  
[IPrintTicketProvider 接口](https://msdn.microsoft.com/library/windows/hardware/ff554375)已添加到通用 (Unidrv) 和 PostScript (PScript5) 打印驱动程序在 Windows Vista 中。

<a href="" id="unidrv-or-pscript5-print-driver-plug-in"></a>Unidrv 或 PScript5 打印驱动程序插件  
Unidrv 和 Pscript5 打印驱动程序具有自定义功能需要插件来添加或删除功能和返回准确的 PrintCapabilities 文档。 自定义插件功能 Unidrv 和打印驱动程序必须支持 PScript5 [IPrintOemPrintTicketProvider 接口](https://msdn.microsoft.com/library/windows/hardware/ff553174)。

<a href="" id="-monolithic-gdi-based-and-xpsdrv-print-drivers"></a> 基于 GDI 的单体和 XPSDrv 打印驱动程序  
XPSDrv 打印驱动程序必须支持[IPrintTicketProvider 接口](https://msdn.microsoft.com/library/windows/hardware/ff554375)。 基于 GDI 的、 整体化打印驱动程序必须支持 IPrintTicketProvider 接口返回的打印机功能和功能的 Win32 函数**DeviceCapabilities**，不提供。

![说明打印驱动程序中的打印功能支持的关系图](images/ptpcarch1.gif)

 

 





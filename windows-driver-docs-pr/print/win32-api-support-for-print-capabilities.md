---
title: 打印功能的 Win32 API 支持
description: 打印功能的 Win32 API 支持
ms.assetid: 1b40cc3e-c6f6-460f-b514-4ef3a001f563
keywords:
- 打印功能 WDK，Win32 API 支持
- DrvDeviceCapabilities
- Win32 应用程序 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51c99493c8b0db8fc0e83aa881f54b4bf981aead
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211869"
---
# <a name="win32-api-support-for-print-capabilities"></a>打印功能的 Win32 API 支持


Windows Vista 打印子系统提供兼容性支持，使 Windows Presentation Foundation (WPF) 应用程序使用基于 GDI 的打印驱动程序，并使基于 Microsoft Win32 的应用程序可以使用 XPSDrv 打印驱动程序。 这种兼容性是通过软件填充层来提供的。 填充码是对数据执行转换操作的软件模块，以便其他不兼容的软件可以互操作。 下图显示了此实现打印功能的数据路径。

![说明打印功能数据流的图示](images/ptpccomp.gif)

[XPSDrv 打印驱动程序](xpsdrv-printer-drivers.md)和基于 GDI 的版本3打印驱动程序均支持[**DrvDeviceCapabilities**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicecapabilities)函数。 当 Win32 应用程序调用 **DrvDeviceCapabilities** 或 **GetDevCap** 函数时，打印子系统将调用 **DrvDeviceCapabilities** 以从打印驱动程序收集设备功能信息。

当 WPF 应用程序从打印驱动程序请求 PrintCapabilities 文档时，打印子系统将执行以下操作之一：

-   如果打印驱动程序支持 [IPrintTicketProvider 接口](/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))，打印子系统将使用 [**IPrintTicketProvider：： GetPrintCapabilities**](/previous-versions/windows/hardware/drivers/ff554365(v=vs.85)) 方法查询 PrintCapabilities 文档的打印驱动程序。

-   如果打印驱动程序不支持 **IPrintTicketProvider** 接口，打印票证管理器将查询打印驱动程序的 [**DrvDeviceCapabilities**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicecapabilities) 函数，并使用返回的信息创建返回到应用程序的 PrintTicket 文档。

有关 Microsoft 打印驱动程序如何支持 **IPrintTicketProvider** 接口的详细信息，请参阅 [Windows Vista 中的打印机驱动程序和插件接口设计](printer-driver-and-plug-in-helper-interfaces.md)。

 


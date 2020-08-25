---
title: 打印票证与 Win 32 应用程序的兼容性
description: 打印票证与 Win 32 应用程序的兼容性
ms.assetid: 3e358f8a-e950-4da0-b8ef-4e350ea28091
keywords:
- Win32 应用程序 WDK 打印
- 打印票证 WDK，Win32 应用程序
- 打印票证 WDK，XPSDrv
- 打印入场券 WDK，基于 GDI 的打印驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80b23e943dcfa2f70e65b58f24eeff765d521945
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802437"
---
# <a name="print-ticket-compatibility-with-win-32-applications"></a>打印票证与 Win 32 应用程序的兼容性


在基于 Microsoft Win32 的应用程序和基于 GDI 的打印驱动程序中使用打印票证时，必须考虑以下兼容性方案：

<a href="" id="win32-based-applications-that-are-printing-to-xpsdrv-print-drivers"></a>将打印到 XPSDrv 打印驱动程序的基于 Win32 的应用程序  
当无法识别打印票证文档的基于 Win32 的应用程序打印到 XPSDrv 打印驱动程序时，"GDI 到 XPS 转换" 模块将从基于 Win32 的应用程序所做的 DDI 调用创建一个 XPS 假脱机文件。 Windows Vista 打印支持还可以创建基于 Win32 应用程序使用的 DEVMODE 结构的打印票证，并将其插入到为文档创建的 XPS 假脱机文件中。 GDI 到 XPS 转换只能转换 DEVMODE 结构的公共部分。 该转换使用适当的 XML 二进制编码将私有 DEVMODE 作为 (BLOB) 的二进制大型对象嵌入打印票证。 可以从 DEVMODEW 票证转换中的打印票证将二进制 BLOB 还原到 [**DEVMODEW**](https://docs.microsoft.com/windows/win32/api/wingdi/ns-wingdi-devmodew) 结构的私有部分。

对于 XPSDrv 打印驱动程序，从基于 Win32 的应用程序发送的文档与从 Windows Presentation Foundation (WPF) 应用程序发送的文档并不不同，因为这两个文档以 XPS 假脱机文件格式进行后台处理。

<a href="" id="wpf-applications-that-are-printing-to-gdi-based-print-drivers"></a>打印到基于 GDI 的打印驱动程序的 WPF 应用程序  
当 WPF 应用程序将包含打印票证的文档打印到不支持打印票证的基于 GDI 的打印驱动程序时，Windows Vista 打印支持会将 WPF 应用程序传递的 XPS 文档转换为 [EMF](emf-data-type.md) 文件，并将每个打印票证转换为 DEVMODE 结构。

对于 GDI 打印驱动程序，来自 WPF 应用程序的打印作业与 Win32 应用程序发送的打印作业不同。

 

 





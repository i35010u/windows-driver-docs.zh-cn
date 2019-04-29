---
title: 打印票证与 Win 32 应用程序的兼容性
description: 打印票证与 Win 32 应用程序的兼容性
ms.assetid: 3e358f8a-e950-4da0-b8ef-4e350ea28091
keywords:
- Win32 应用程序 WDK 打印
- 打印票证 WDK，Win32 应用程序
- 打印票证 WDK，XPSDrv
- 打印票证 WDK，基于 GDI 的打印驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af24bec9343a18fc82e34a07581453aa5a833dfa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362713"
---
# <a name="print-ticket-compatibility-with-win-32-applications"></a>打印票证与 Win 32 应用程序的兼容性


当您使用 Microsoft 基于 Win32 的应用程序和基于 GDI 的打印驱动程序中的打印票证时，必须考虑以下的兼容性方案：

<a href="" id="win32-based-applications-that-are-printing-to-xpsdrv-print-drivers"></a>基于 Win32 的应用程序的打印到 XPSDrv 打印驱动程序  
当基于 Win32 的应用程序，并不知道的打印票证文档打印到 XPSDrv 打印驱动程序时，GDI 到 XPS 转换模块从基于 Win32 的应用程序进行的 DDI 调用创建 XPS 假脱机文件。 Windows Vista 打印支持还会创建 DEVMODE 结构基于 Win32 的应用程序使用，并将其插入到文档创建 XPS 假脱机文件为基础的打印票证。 GDI 到 XPS 转换可以将转换仅 DEVMODE 结构的公共部分。 转换将嵌入到作为二进制大型对象 (BLOB) 的打印票证的专用 DEVMODE 使用相应的 XML 二进制编码。 可以将二进制 BLOB 还原到的专用部分[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)从 DEVMODEW 打印票证转换中的打印票证的结构。

XPSDrv 打印驱动程序，从基于 Win32 的应用程序发送的文档不是不同于从 Windows Presentation Foundation (WPF) 应用程序发送，因为这两个文档假脱机保存 XPS 后台打印文件格式的文档。

<a href="" id="wpf-applications-that-are-printing-to-gdi-based-print-drivers"></a>WPF 应用程序，打印于基于 GDI 的打印驱动程序  
Windows Vista 打印支持在 WPF 应用程序将打印到基于 GDI 的打印驱动程序不支持打印票证包含打印票证的文档，将 WPF 应用程序传递到 XPS 文档转换[EMF](emf-data-type.md)文件和转换到 DEVMODE 结构的每个打印票证。

GDI 打印驱动程序，打印作业从 WPF 应用程序不是不同于 Win32 应用程序发送打印作业。

 

 





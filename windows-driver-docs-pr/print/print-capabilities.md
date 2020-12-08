---
title: 打印功能
description: 打印功能
keywords:
- 打印功能 WDK，关于打印功能
- XML PrintCapabilities WDK 打印
- PrintCapabilities 文档 WDK 打印
- IPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64780e0d63d614ca9e632f69505d011341a71cae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807495"
---
# <a name="print-capabilities"></a>打印功能


通过使用打印功能技术，打印驱动程序可以将其功能作为 XML 文档中的一组元素返回。 当应用程序调用 **DeviceCapabilities** 或 **GetDeviceCaps** 函数时，早期版本的打印驱动程序返回其功能信息。 不过，这些 Microsoft Win32 函数会受到限制，因为它们只返回一组固定的打印机功能和设置的信息，并且可以返回有关每个函数调用的一个功能或设置的信息。

与此相反，XML PrintCapabilities 文档的灵活性更高，设计用于支持新的打印机功能。 PrintCapabilities 函数还在一个函数调用中返回整个 XML PrintCapabilities 文档。

本部分介绍了打印功能的以下方面：

[打印功能体系结构](print-capabilities-architecture.md)

[打印功能的 Win32 API 支持](win32-api-support-for-print-capabilities.md)

[Unidrv 和 PScript5 打印驱动程序中的打印功能](print-capabilities-in-unidrv-and-pscript5-print-drivers.md)

[打印驱动程序插件支持](print-driver-plug-in-support.md)

[基于 GDI 的一体式打印驱动程序中的打印功能支持](print-capabilities-support-in-gdi-based--monolithic-print-drivers.md)

 

 





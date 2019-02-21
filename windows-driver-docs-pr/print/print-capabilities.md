---
title: 打印功能
description: 打印功能
ms.assetid: 8ccbdab3-5be4-4ee1-9798-3b90e8b5b4d4
keywords:
- 打印功能 WDK，有关打印功能
- XML PrintCapabilities WDK 打印
- PrintCapabilities 文档 WDK 打印
- IPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e9ce7aa80bd5a3d552d751a0ee6df8991f63ec1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526576"
---
# <a name="print-capabilities"></a>打印功能


通过使用打印功能技术，打印驱动程序可以返回其功能作为一组 XML 文档中的元素。 早期版本的打印驱动程序应用程序调用时返回了其功能的信息**DeviceCapabilities**或**GetDeviceCaps**函数。 这些 Microsoft Win32 函数，但是，非常有限，因为它们返回有关一组固定的打印机功能和设置的唯一信息并可以返回有关只能有一个功能或设置每个函数调用的信息。

与此相反，XML PrintCapabilities 文档则灵活得多，专为支持新的打印机功能。 PrintCapabilities 函数也返回一个函数调用中的整个 XML PrintCapabilities 文档。

本部分介绍了打印功能的以下方面：

[打印功能体系结构](print-capabilities-architecture.md)

[Win32 API 对打印功能的支持](win32-api-support-for-print-capabilities.md)

[打印 Unidrv 和 PScript5 打印驱动程序中的功能](print-capabilities-in-unidrv-and-pscript5-print-drivers.md)

[打印驱动程序插件支持](print-driver-plug-in-support.md)

[基于 GDI 的、 整体化打印驱动程序中的打印功能支持](print-capabilities-support-in-gdi-based--monolithic-print-drivers.md)

 

 





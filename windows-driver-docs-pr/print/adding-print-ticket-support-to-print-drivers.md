---
title: 将打印票证支持添加到打印驱动程序
description: 将打印票证支持添加到打印驱动程序
ms.assetid: ef4db930-2b4c-40b9-b1f4-85767b7f6855
keywords:
- 自定义 WDK、 打印票证的打印机驱动程序
- 自定义打印机驱动程序 WDK、 打印票证
- 打印票证 WDK，添加对的支持
- IPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17456eaef415b5570a65695bca153e698f62c1e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354088"
---
# <a name="adding-print-ticket-support-to-print-drivers"></a>将打印票证支持添加到打印驱动程序


若要完全支持[打印票证和打印功能技术](print-ticket-and-print-capabilities-technologies.md)，打印驱动程序必须：

-   支持[IPrintTicketProvider 接口](https://msdn.microsoft.com/library/windows/hardware/ff554375)根据需要，提供[打印功能](print-capabilities.md)打印机的文档。

-   支持[IPrintOemPrintTicketProvider 接口](https://msdn.microsoft.com/library/windows/hardware/ff553174)中打印驱动程序插件。

-   使用[打印票证](print-ticket.md)时处理打印作业的信息。

打印驱动程序支持 IPrintTicketProvider 接口来实现上述列表中的前两个项，但不能解决的最后一项。 打印驱动程序必须读取和处理的打印票证 XPS 文档中的设置，以便这些设置会影响打印的文档。 有关实现此支持的详细信息，请参阅[XPSDrv 呈现模块中的打印票证支持](print-ticket-support-in-the-xpsdrv-render-module.md)。

**请注意**  基于 GDI 的版本 3 打印驱动程序不需要将打印票证支持添加到驱动程序，因为打印子系统将 PrintTicket 对象转换为等效[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)打印驱动程序的结构。

 

 

 





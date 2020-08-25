---
title: 打印票证
description: 打印票证
ms.assetid: dd18d0ef-c1f7-4a35-a420-2da102fb07f4
keywords:
- PrintTicket 文档 WDK
- 打印票证 WDK，PrintTicket 文档
- 文档说明 WDK 打印
- 打印作业 WDK，打印票证
- 作业 WDK 打印，打印票证
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55e2a2929c9b44c2190470bd9aeaf118e9dc37ee
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802541"
---
# <a name="print-ticket"></a>打印票证


PrintTicket 文档是一个 XML 文档，用于描述如何打印文档或文档部分。 PrintTicket 文档可与文档中的打印作业、文档或页相关联。 可以将 PrintTicket 文档作为 PrintTicket 部分添加到 XPS 文档中，并随文件中的文档内容一起保存。 当应用程序对文档进行后台打印以便打印时，还可以将 PrintTicket 文档添加到文档中。

转换函数使您能够在 Microsoft Win32 应用程序中打印票证使用情况。 函数可用于将打印票证转换为 [**DEVMODEW**](https://docs.microsoft.com/windows/win32/api/wingdi/ns-wingdi-devmodew) 结构，并将 DEVMODEW 结构转换回打印票证。

本节包含下列主题：

[打印票证组织](print-ticket-organization.md)

[打印票证与 Win 32 应用程序的兼容性](print-ticket-compatibility-with-win-32-applications.md)

[打印驱动程序中的打印票证处理](print-ticket-processing-in-the-print-driver.md)

[Unidrv 和 PScript5 打印驱动程序中的打印票证支持](print-ticket-support-in-unidrv-and-pscript5-print-drivers.md)

 

 





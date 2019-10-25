---
title: 将打印票证支持添加到打印驱动程序
description: 将打印票证支持添加到打印驱动程序
ms.assetid: ef4db930-2b4c-40b9-b1f4-85767b7f6855
keywords:
- 打印机驱动程序自定义 WDK，打印票证
- 自定义打印机驱动程序 WDK，打印票证
- 打印入场券 WDK，添加对的支持
- IPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75be180509e4c22a8d1436eb2ed6ffb6745cb968
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843261"
---
# <a name="adding-print-ticket-support-to-print-drivers"></a>将打印票证支持添加到打印驱动程序


若要完全支持[打印票证和打印功能技术](print-ticket-and-print-capabilities-technologies.md)，打印驱动程序必须：

-   根据需要支持[IPrintTicketProvider 接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))，以便提供打印机的[打印功能](print-capabilities.md)文档。

-   支持 "打印驱动程序" 插件中的[IPrintOemPrintTicketProvider 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintoemprintticketprovider)。

-   处理打印作业时使用[打印票证](print-ticket.md)信息。

支持 IPrintTicketProvider 接口的打印驱动程序将完成前面的列表中的前两项，但不会对最后一项进行寻址。 打印驱动程序必须读取并处理 XPS 文档中打印票证的设置，以便这些设置影响打印的文档。 有关实现此支持的详细信息，请参阅[XPSDrv Render 模块中的打印票证支持](print-ticket-support-in-the-xpsdrv-render-module.md)。

**请注意**   基于 GDI 的打印驱动程序不需要将打印票证支持添加到驱动程序，因为打印子系统将 PrintTicket 对象转换为打印驱动程序的等效[**DEVMODEW**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)结构。

 

 

 





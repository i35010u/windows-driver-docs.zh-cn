---
title: ValidatePrintTicket 概述
description: 每个插件调用 IPrintOemPrintTicketProvider::ValidatePrintTicket 方法来验证 PrintTicket。
ms.assetid: 3a4cf946-c931-4f71-9f1a-4efec4dfe866
keywords:
- ValidatePrintTicket
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67fbaa90896d86d8cde63fd7cea429f181bb6d99
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379106"
---
# <a name="validateprintticket-overview"></a>ValidatePrintTicket 概述


Unidrv 和 PScript5 打印驱动程序验证通过使用下面的图和列表显示序列的打印票证。

![说明如何 unidrv 和 pscript5 打印驱动程序的关系图验证的打印票证](images/ptpcvalpt-uml.gif)

1.  每个插件，请调用[ **IPrintOemPrintTicketProvider::ExpandIntentOptions** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemprintticketprovider-expandintentoptions)方法。

2.  调用[ **IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemprintticketprovider-convertprinttickettodevmode)方法。

3.  每个插件，请调用**IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode**要转换的专用部分[ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)结构。

4.  验证公共和专用的部分 DEVMODEW 结构 Unidrv 或 PScript5 打印驱动程序支持。

5.  每个插件，请验证 DEVMODEW 结构的私有部分。

6.  调用[ **IPrintTicketProvider::ConvertPrintTicketToDevMode** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554363(v=vs.85))方法。

7.  每个插件，请调用[ **IPrintOemPrintTicketProvider::ConvertDevModeToPrintTicket** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553161(v=vs.85))方法将 DEVMODEW 结构的专用部分。

8.  每个插件，请调用[ **IPrintOemPrintTicketProvider::ValidatePrintTicket** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553184(v=vs.85))方法来验证 PrintTicket。

 

 





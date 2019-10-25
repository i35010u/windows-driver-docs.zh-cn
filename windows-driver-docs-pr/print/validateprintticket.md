---
title: ValidatePrintTicket 概述
description: 每个插件将调用 IPrintOemPrintTicketProvider：： ValidatePrintTicket 方法来验证 PrintTicket。
ms.assetid: 3a4cf946-c931-4f71-9f1a-4efec4dfe866
keywords:
- ValidatePrintTicket
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a528f89f55339e656024eaf417c248dca398453b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844758"
---
# <a name="validateprintticket-overview"></a>ValidatePrintTicket 概述


Unidrv 和 PScript5 打印驱动程序使用以下插图和 list 显示的序列来验证打印票证。

![说明 unidrv 和 pscript5 打印驱动程序如何验证打印票证的关系图](images/ptpcvalpt-uml.gif)

1.  对于每个插件，请调用[**IPrintOemPrintTicketProvider：： ExpandIntentOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemprintticketprovider-expandintentoptions)方法。

2.  调用[**IPrintOemPrintTicketProvider：： ConvertPrintTicketToDevMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemprintticketprovider-convertprinttickettodevmode)方法。

3.  对于每个插件，请调用**IPrintOemPrintTicketProvider：： ConvertPrintTicketToDevMode**来转换[**DEVMODEW**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)结构的私有部分。

4.  验证 Unidrv 或 PScript5 打印驱动程序支持的 DEVMODEW 结构的公共和私有部分。

5.  对于每个插件，验证 DEVMODEW 结构的私有部分。

6.  调用[**IPrintTicketProvider：： ConvertPrintTicketToDevMode**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554363(v=vs.85))方法。

7.  对于每个插件，请调用[**IPrintOemPrintTicketProvider：： ConvertDevModeToPrintTicket**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553161(v=vs.85))方法来转换 DEVMODEW 结构的私有部分。

8.  对于每个插件，请调用[**IPrintOemPrintTicketProvider：： ValidatePrintTicket**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553184(v=vs.85))方法来验证 PrintTicket。

 

 





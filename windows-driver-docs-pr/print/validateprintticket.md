---
title: ValidatePrintTicket 概述
description: 每个插件将调用 IPrintOemPrintTicketProvider：： ValidatePrintTicket 方法来验证 PrintTicket。
keywords:
- ValidatePrintTicket
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57d51a3c9840d624b91ff5924b9445bc63e47905
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785865"
---
# <a name="validateprintticket-overview"></a>ValidatePrintTicket 概述


Unidrv 和 PScript5 打印驱动程序使用以下插图和 list 显示的序列来验证打印票证。

![说明 unidrv 和 pscript5 打印驱动程序如何验证打印票证的关系图](images/ptpcvalpt-uml.gif)

1.  对于每个插件，请调用 [**IPrintOemPrintTicketProvider：： ExpandIntentOptions**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemprintticketprovider-expandintentoptions) 方法。

2.  调用 [**IPrintOemPrintTicketProvider：： ConvertPrintTicketToDevMode**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemprintticketprovider-convertprinttickettodevmode) 方法。

3.  对于每个插件，请调用 **IPrintOemPrintTicketProvider：： ConvertPrintTicketToDevMode** 来转换 [**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devmodew) 结构的私有部分。

4.  验证 Unidrv 或 PScript5 打印驱动程序支持的 DEVMODEW 结构的公共和私有部分。

5.  对于每个插件，验证 DEVMODEW 结构的私有部分。

6.  调用 [**IPrintTicketProvider：： ConvertPrintTicketToDevMode**](/previous-versions/windows/hardware/drivers/ff554363(v=vs.85)) 方法。

7.  对于每个插件，请调用 [**IPrintOemPrintTicketProvider：： ConvertDevModeToPrintTicket**](/previous-versions/windows/hardware/drivers/ff553161(v=vs.85)) 方法来转换 DEVMODEW 结构的私有部分。

8.  对于每个插件，请调用 [**IPrintOemPrintTicketProvider：： ValidatePrintTicket**](/previous-versions/windows/hardware/drivers/ff553184(v=vs.85)) 方法来验证 PrintTicket。

 


---
title: ValidatePrintTicket 概述
description: 每个插件调用 IPrintOemPrintTicketProvider::ValidatePrintTicket 方法来验证 PrintTicket。
ms.assetid: 3a4cf946-c931-4f71-9f1a-4efec4dfe866
keywords:
- ValidatePrintTicket
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5359a1c015f0b25397bff0d2a0911e7989163d54
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387813"
---
# <a name="validateprintticket-overview"></a>ValidatePrintTicket 概述


Unidrv 和 PScript5 打印驱动程序验证通过使用下面的图和列表显示序列的打印票证。

![说明如何 unidrv 和 pscript5 打印驱动程序的关系图验证的打印票证](images/ptpcvalpt-uml.gif)

1.  每个插件，请调用[ **IPrintOemPrintTicketProvider::ExpandIntentOptions** ](https://msdn.microsoft.com/library/windows/hardware/ff553168)方法。

2.  调用[ **IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode** ](https://msdn.microsoft.com/library/windows/hardware/ff553167)方法。

3.  每个插件，请调用**IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode**要转换的专用部分[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)结构。

4.  验证公共和专用的部分 DEVMODEW 结构 Unidrv 或 PScript5 打印驱动程序支持。

5.  每个插件，请验证 DEVMODEW 结构的私有部分。

6.  调用[ **IPrintTicketProvider::ConvertPrintTicketToDevMode** ](https://msdn.microsoft.com/library/windows/hardware/ff554363)方法。

7.  每个插件，请调用[ **IPrintOemPrintTicketProvider::ConvertDevModeToPrintTicket** ](https://msdn.microsoft.com/library/windows/hardware/ff553161)方法将 DEVMODEW 结构的专用部分。

8.  每个插件，请调用[ **IPrintOemPrintTicketProvider::ValidatePrintTicket** ](https://msdn.microsoft.com/library/windows/hardware/ff553184)方法来验证 PrintTicket。

 

 





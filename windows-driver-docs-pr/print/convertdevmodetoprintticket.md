---
title: ConvertDevModeToPrintTicket 概述
description: 对于安装的每个打印驱动程序插件，将调用 ConvertDevModeToPrintTicket 方法。
ms.assetid: 71387d8b-60ce-4deb-a20b-9d7b0b7be230
keywords:
- ConvertDevModeToPrintTicket
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b64cec1bdae0ec765913817258b5d61bb4e505e5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210615"
---
# <a name="convertdevmodetoprintticket-overview"></a>ConvertDevModeToPrintTicket 概述


Unidrv 和 PScript5 打印驱动程序通过使用驱动程序所支持的 [**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devmodew) 结构的公共和私有部分中的元素来创建打印票证。 对于安装的每个打印驱动程序插件，都将调用 [**IPrintOemPrintTicketProvider：： ConvertDevModeToPrintTicket**](/previous-versions/windows/hardware/drivers/ff553161(v=vs.85)) 方法。

下图显示了驱动程序调用 ConvertDevModeToPrintTicket 时，对 IPrintOemPrintTicketProvider：： ConvertDevModeToPrintTicket 的调用的顺序。

![convertdevmodetoprintticket 调用序列](images/ptpcdm2pt-uml.gif)

 


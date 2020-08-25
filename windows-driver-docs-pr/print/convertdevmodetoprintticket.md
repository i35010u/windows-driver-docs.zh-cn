---
title: ConvertDevModeToPrintTicket 概述
description: 对于安装的每个打印驱动程序插件，将调用 ConvertDevModeToPrintTicket 方法。
ms.assetid: 71387d8b-60ce-4deb-a20b-9d7b0b7be230
keywords:
- ConvertDevModeToPrintTicket
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2303afe1be8e0654ca111f3fc0168108bd254ea9
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802615"
---
# <a name="convertdevmodetoprintticket-overview"></a>ConvertDevModeToPrintTicket 概述


Unidrv 和 PScript5 打印驱动程序通过使用驱动程序所支持的 [**DEVMODEW**](https://docs.microsoft.com/windows/win32/api/wingdi/ns-wingdi-devmodew) 结构的公共和私有部分中的元素来创建打印票证。 对于安装的每个打印驱动程序插件，都将调用 [**IPrintOemPrintTicketProvider：： ConvertDevModeToPrintTicket**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553161(v=vs.85)) 方法。

下图显示了驱动程序调用 ConvertDevModeToPrintTicket 时，对 IPrintOemPrintTicketProvider：： ConvertDevModeToPrintTicket 的调用的顺序。

![convertdevmodetoprintticket 调用序列](images/ptpcdm2pt-uml.gif)

 

 





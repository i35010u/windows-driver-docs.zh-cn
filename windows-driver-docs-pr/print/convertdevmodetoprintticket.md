---
title: ConvertDevModeToPrintTicket 概述
description: ConvertDevModeToPrintTicket 方法调用的每个打印驱动程序插件已安装。
ms.assetid: 71387d8b-60ce-4deb-a20b-9d7b0b7be230
keywords:
- ConvertDevModeToPrintTicket
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6d07230ca976330dd9f45683661227bc767bf39
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374667"
---
# <a name="convertdevmodetoprintticket-overview"></a>ConvertDevModeToPrintTicket 概述


Unidrv 和 PScript5 打印驱动程序使用的公共和私有部分中的元素创建打印票证[ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)驱动程序支持的结构。 [ **IPrintOemPrintTicketProvider::ConvertDevModeToPrintTicket** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553161(v=vs.85))为每个打印驱动程序插件已安装的调用方法。

下图显示对 IPrintOemPrintTicketProvider::ConvertDevModeToPrintTicket 调用的顺序时，驱动程序调用 ConvertDevModeToPrintTicket。

![convertdevmodetoprintticket 调用的序列](images/ptpcdm2pt-uml.gif)

 

 





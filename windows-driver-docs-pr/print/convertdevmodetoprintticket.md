---
title: ConvertDevModeToPrintTicket 概述
description: ConvertDevModeToPrintTicket 方法调用的每个打印驱动程序插件已安装。
ms.assetid: 71387d8b-60ce-4deb-a20b-9d7b0b7be230
keywords:
- ConvertDevModeToPrintTicket
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e1575700126bd6e775f7519cc5f53dc1acabf2d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547136"
---
# <a name="convertdevmodetoprintticket-overview"></a>ConvertDevModeToPrintTicket 概述


Unidrv 和 PScript5 打印驱动程序使用的公共和私有部分中的元素创建打印票证[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)驱动程序支持的结构。 [ **IPrintOemPrintTicketProvider::ConvertDevModeToPrintTicket** ](https://msdn.microsoft.com/library/windows/hardware/ff553161)为每个打印驱动程序插件已安装的调用方法。

下图显示对 IPrintOemPrintTicketProvider::ConvertDevModeToPrintTicket 调用的顺序时，驱动程序调用 ConvertDevModeToPrintTicket。

![convertdevmodetoprintticket 调用的序列](images/ptpcdm2pt-uml.gif)

 

 





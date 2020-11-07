---
title: 动态生成的打印机命令
description: 动态生成的打印机命令
ms.assetid: ba395716-6906-4f23-a050-79d808ccd44b
keywords:
- Unidrv，动态生成的命令
- 动态生成的打印命令 WDK Unidrv
- GPD 文件 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3566b8e1a90dccc1a4eea28f96a5a75f4ba9b0be
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361533"
---
# <a name="dynamically-generated-printer-commands"></a>动态生成的打印机命令





对于 Unidrv 微型驱动程序，每次在 *GPD* 文件中指定 [打印机命令](printer-commands.md)时，可以使用以下两种方法之一：

-   将命令字符串放在 GPD 文件中。

    将命令字符串放在 GPD 文件中时，Unidrv 会在适当的时间将命令发送到打印后台处理程序。 这些命令字符串可以包含标准变量，这些变量 Unidrv 在发送命令之前计算。

-   提供回调函数。

    如果提供回调函数，则在发送命令时，Unidrv 会调用函数，并且该函数负责将命令发送到打印后台处理程序。 这使你能够包含动态生成命令字符串并将其发送到打印机的代码。

若要将命令字符串放在 GPD 文件中，需要在 \* 命令的命令条目中包含 Cmd 特性 \* 。

若要提供动态生成命令字符串的代码，必须执行以下操作：

-   提供实现 [**IPrintOemUni：： CommandCallback**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-commandcallback) 方法的呈现插件。

-   在 \* \* GPD 文件中的命令项内，包括 CallbackID 命令特性和 Params 特性（可选） \* 。

当 Unidrv 准备好发出打印机命令时，它会检查微型驱动程序数据库，以确定是否已使用 \* Cmd 属性或 CallbackID 属性指定该命令 \* 。 在前一种情况下，Unidrv 将命令字符串发送到打印后台处理程序。 在后一种情况下，Unidrv 调用 **IPrintOemUni：： CommandCallback** 方法，将 \* CallbackID 和 \* Params 值作为输入参数传递。

 


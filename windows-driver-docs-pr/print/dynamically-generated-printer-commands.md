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
ms.openlocfilehash: 6f2f6a7d9122ddb1565db3dc37a121497fed8d51
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841637"
---
# <a name="dynamically-generated-printer-commands"></a>动态生成的打印机命令





每次为 Unidrv 微型驱动程序指定打印机命令文件时，都可以使用以下两种方法之一：

-   将命令字符串放在 GPD 文件中。

    将命令字符串放在 GPD 文件中时，Unidrv 会在适当的时间将命令发送到打印后台处理程序。 这些命令字符串可以包含标准变量，这些变量 Unidrv 在发送命令之前计算。

-   提供回调函数。

    如果提供回调函数，则在发送命令时，Unidrv 会调用函数，并且该函数负责将命令发送到打印后台处理程序。 这使你能够包含动态生成命令字符串并将其发送到打印机的代码。

若要将命令字符串放在 GPD 文件中，需要在命令的 \*命令条目中包含一个 \*Cmd 特性。

若要提供动态生成命令字符串的代码，必须执行以下操作：

-   提供实现[**IPrintOemUni：： CommandCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-commandcallback)方法的呈现插件。

-   在 GPD 文件中的命令的 \*命令项内，包括一个 \*CallbackID 命令特性，还可以选择 \*Params 特性。

当 Unidrv 准备好发出打印机命令时，它会检查微型驱动程序数据库，以确定是否已使用 \*Cmd 属性或 \*CallbackID 特性指定了命令。 在前一种情况下，Unidrv 将命令字符串发送到打印后台处理程序。 在后一种情况下，Unidrv 调用**IPrintOemUni：： CommandCallback**方法，将 \*CallbackID 和 \*Params 值作为输入参数传递。

 

 





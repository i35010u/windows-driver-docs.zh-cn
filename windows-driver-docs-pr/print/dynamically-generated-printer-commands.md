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
ms.openlocfilehash: 2224e35dd11d04be01dd7a62edb5a6df49812f29
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568549"
---
# <a name="dynamically-generated-printer-commands"></a>动态生成的打印机命令





Unidrv 微型驱动程序，用于指定打印机命令文件每次可以使用以下两种方法之一：

-   将命令字符串放在 GPD 文件。

    当你将命令字符串放在 GPD 文件中时，Unidrv 将在适当的时间将命令发送到打印后台处理程序上。 这些命令字符串可以包含 Unidrv 计算，然后将命令发送的标准变量。

-   提供一个回调函数。

    如果提供的回调函数，Unidrv 时就可以发送命令时，该函数负责将命令发送到打印后台处理程序调用函数。 这可以包含动态生成的命令字符串，然后将它发送到打印机的代码。

若要将命令字符串放在 GPD 文件，您需要包括\*Cmd 属性中命令的\*命令项。

若要提供动态生成的命令字符串的代码，必须执行以下操作：

-   提供用于实现的插件呈现[ **IPrintOemUni::CommandCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff554216)方法。

-   包括\*CallbackID 命令属性和 （可选） \*Params 属性，该命令中的\*命令 GPD 文件中的条目。

准备就绪，可以发出打印机命令 Unidrv 时，它会检查微型驱动程序数据库，以确定该命令指定与\*Cmd 属性或使用\*CallbackID 属性。 在前一种情况，Unidrv 将命令字符串发送到打印后台处理程序。 在后一种情况下，调用 Unidrv **IPrintOemUni::CommandCallback**方法，传递\*CallbackID 和\*参数值作为输入的参数。

 

 





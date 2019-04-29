---
title: 打印机命令
description: 打印机命令
ms.assetid: 4f47ae57-cfca-4670-823e-526e2f40de82
keywords:
- Unidrv 命令
- GPD 文件 WDK Unidrv，打印机命令
- WDK Unidrv 命令
- 打印机命令 WDK Unidrv
- 打印机的 WDK Unidrv 命令有关打印机命令
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18de40713521aa72349c99cf97836bb3f5d9c205
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380530"
---
# <a name="printer-commands"></a>打印机命令





GPD 语言提供了每个预定义的命令名称通常使用的打印机操作。 此外，可以为特定于设备的定义自定义的命令[打印机选项](printer-options.md)。

可以在两种方式之一中实现每个打印机命令：

-   可以将特定于设备的命令字符串放在 GPD 文件中。 Unidrv 在适当的时间将命令字符串发送到打印后台处理程序。

-   您可以实现[ **IPrintOemUni::CommandCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff554216) COM 方法，动态生成的命令字符串。 Unidrv 每当时，它将命令发送到后台处理程序调用的方法。 有关详细信息请参阅[动态生成打印机命令](dynamically-generated-printer-commands.md)中[自定义 Microsoft 的打印机驱动程序](customizing-microsoft-s-printer-drivers.md)。

以下主题介绍如何在 GPD 文件中指定打印机命令：

[命令条目格式](command-entry-format.md)

[命令名称](command-names.md)

[命令属性](command-attributes.md)

[命令字符串格式](command-string-format.md)

[命令执行顺序](command-execution-order.md)

 

 





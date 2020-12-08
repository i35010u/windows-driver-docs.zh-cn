---
title: 打印机命令
description: 打印机命令
keywords:
- Unidrv，命令
- GPD 文件 WDK Unidrv，打印机命令
- 命令 WDK Unidrv
- 打印机命令 WDK Unidrv
- 打印机命令 WDK Unidrv，关于打印机命令
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7627fda0e2d8081420e1d239b34881fd512bbd33
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807355"
---
# <a name="printer-commands"></a>打印机命令





GPD 语言为每个常用打印机操作提供预定义的命令名称。 此外，可以为特定于设备的 [打印机选项](printer-options.md)定义自定义命令。

可以通过以下两种方式之一来实现每个打印机命令：

-   可以在 GPD 文件中放置特定于设备的命令字符串。 Unidrv 在适当的时间将命令字符串发送到打印后台处理程序。

-   可以实现 [**IPrintOemUni：： CommandCallback**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-commandcallback) COM 方法，这会动态生成命令字符串。 只要需要将命令发送到后台处理程序，Unidrv 就会调用方法。 有关详细信息，请参阅[自定义 Microsoft 的打印机驱动程序](customizing-microsoft-s-printer-drivers.md)中[动态生成的打印机命令](dynamically-generated-printer-commands.md)。

以下主题介绍如何在 GPD 文件中指定打印机命令：

[命令项格式](command-entry-format.md)

[命令名称](command-names.md)

[命令属性](command-attributes.md)

[命令字符串格式](command-string-format.md)

[命令执行顺序](command-execution-order.md)

 


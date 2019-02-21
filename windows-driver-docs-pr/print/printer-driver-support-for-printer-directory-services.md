---
title: 打印机目录服务的打印机驱动程序支持
description: 打印机目录服务的打印机驱动程序支持
ms.assetid: 6b0b3cda-a9e5-458d-b5e2-89667059bde4
keywords:
- 目录服务 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99a55de61a9bf2b9e77bee24b5c4ef2b0016ec90
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520169"
---
# <a name="printer-driver-support-for-printer-directory-services"></a>打印机目录服务的打印机驱动程序支持





打印机驱动程序不负责发布到目录服务的打印队列。 Microsoft Windows 2000 和更高版本的打印文件夹创建的打印队列对象 (通过调用后台处理程序的**SetPrinter**函数) 在安装打印机的过程。 (请参阅[发布打印队列](print-spooler-support-for-printer-directory-services.md#ddk-publishing-print-queues-gg)。)

打印队列属性发布，以便用户可以通过使用搜索具有特定属性的打印机**搜索**任务栏上的选项**启动**菜单。 打印文件夹发布的打印机功能从 DriverCapabilities 都可与它的部分，而不是全部。 发布用于浏览目的被视为非常有用的功能。

打印机驱动程序可以添加或修改打印队列对象的属性信息。 由标识可以发布的打印队列属性**SPLDS\_**-前缀 winspool.h 中定义的常量。 若要添加或修改打印机属性，您的驱动程序必须使用这些预定义的属性的名称标识符。

若要添加或修改打印队列对象的属性信息，请执行以下步骤：

1.  将属性名称和值添加到注册表中，在 SPLDS\_驱动程序\_键，通过调用后台处理程序的**SetPrinterDataEx**函数。

2.  调用后台处理程序的**SetPrinter**函数，使用的打印机的输入结构\_信息\_7 （Windows SDK 文档中所述） 和操作的 DSPRINT\_更新，以通知后台处理程序它应更新已发布的打印队列对象。 (驱动程序不应指定操作的 DSPRINT\_发布。)

应在打印机驱动程序中实现这些步骤[ **DrvPrinterEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff548564)函数，在函数收到打印机时\_事件\_INITIALIZE 事件。

如果驱动程序必须获取的当前值为打印机的已发布属性，则应调用**GetPrinterDataEx**或**EnumPrinterDataEx**从注册表中，这是获取信息后台处理程序维护和始终保持最新。 另一种方法是调用**GetPrinter**获取打印队列的对象标识符，然后调用 ADSI 函数来获取已发布的属性的值。 不建议此方法，因为它需要消耗大量的更多资源，并且因为返回的数据可能不始终是最新内容。

 

 





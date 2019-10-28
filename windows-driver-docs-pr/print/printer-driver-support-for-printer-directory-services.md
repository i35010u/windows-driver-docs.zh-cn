---
title: 打印机目录服务的打印机驱动程序支持
description: 打印机目录服务的打印机驱动程序支持
ms.assetid: 6b0b3cda-a9e5-458d-b5e2-89667059bde4
keywords:
- 目录服务 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb957dc2089b39c0c3778cbdf946aa12900abb68
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840434"
---
# <a name="printer-driver-support-for-printer-directory-services"></a>打印机目录服务的打印机驱动程序支持





打印机驱动程序不负责向目录服务发布打印队列。 Microsoft Windows 2000 和更高版本打印文件夹在安装打印机的过程中创建打印队列对象（通过调用后台处理程序的**SetPrinter**函数）。 （请参阅[发布打印队列](print-spooler-support-for-printer-directory-services.md#ddk-publishing-print-queues-gg)。）

将发布打印队列属性，以便用户可以使用任务栏的 "**开始**" 菜单上的 "**搜索**" 选项搜索具有特定属性的打印机。 打印文件夹发布了某些（但不是全部） DriverCapabilities 提供的打印机功能。 仅会发布被认为对浏览目的很有用的功能。

打印机驱动程序可以添加或修改打印队列对象的属性信息。 可发布的打印队列属性由 SPLDS 中定义的 **\_** 的常量标识，在 winspool.drv 中定义。 若要添加或修改打印机属性，您的驱动程序必须使用这些预定义的属性名称标识符。

若要添加或修改打印队列对象的属性信息，请执行以下步骤：

1.  通过调用后台处理程序的**SetPrinterDataEx**函数，将属性名称和值添加到注册表中的 SPLDS\_驱动程序\_键下。

2.  调用后台处理程序的**SetPrinter**函数，其中包含打印机\_信息的输入结构\_7 （Windows SDK 文档中所述）和 DSPRINT\_更新的操作，通知后台处理程序它应更新发布的打印queue 对象。 （驱动程序不应指定 DSPRINT\_"发布" 的操作。）

当函数收到打印机\_事件\_INITIALIZE 事件时，应在打印机驱动程序的[**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent)函数中实现这些步骤。

如果驱动程序必须获取打印机发布的属性的当前值，则它应调用**GetPrinterDataEx**或**EnumPrinterDataEx** ，以从注册表中获取信息，该信息为后台处理程序并始终处于最新状态。 另一种方法是调用**GetPrinter**以获取打印队列的对象标识符，然后调用 ADSI 函数以获取已发布属性的值。 不建议使用此方法，因为它会占用大量的资源，并且返回的数据可能并非总是最新的。

 

 





---
title: 打印机目录服务的打印机驱动程序支持
description: 打印机目录服务的打印机驱动程序支持
ms.assetid: 6b0b3cda-a9e5-458d-b5e2-89667059bde4
keywords:
- 目录服务 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec8d860a59d3aa59eebdcf9d6cba31e68fef9a2d
ms.sourcegitcommit: 88f6e7355de9e0714057020557dc8c7831e90e7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/10/2020
ms.locfileid: "84638444"
---
# <a name="printer-driver-support-for-printer-directory-services"></a>打印机目录服务的打印机驱动程序支持





打印机驱动程序不负责向目录服务发布打印队列。 Microsoft Windows 2000 和更高版本打印文件夹在安装打印机的过程中创建打印队列对象（通过调用后台处理程序的**SetPrinter**函数）。

将发布打印队列属性，以便用户可以使用任务栏的 "**开始**" 菜单上的 "**搜索**" 选项搜索具有特定属性的打印机。 打印文件夹发布了某些（但不是全部） DriverCapabilities 提供的打印机功能。 仅会发布被认为对浏览目的很有用的功能。

打印机驱动程序可以添加或修改打印队列对象的属性信息。 可发布的打印队列属性由 winspool.drv 中定义的**SPLDS \_ **前缀常量标识。 若要添加或修改打印机属性，您的驱动程序必须使用这些预定义的属性名称标识符。

若要添加或修改打印队列对象的属性信息，请执行以下步骤：

1.  \_ \_ 通过调用后台处理程序的**SetPrinterDataEx**函数，将属性名称和值添加到注册表中的 SPLDS DRIVER 项下。

1.  调用后台处理程序的**SetPrinter**函数，该函数的输入结构为打印机 \_ 信息 \_ 7 （如 Windows SDK 文档中所述）和 DSPRINT \_ UPDATE 的操作，用于通知后台处理程序它应更新已发布的打印队列对象。 （驱动程序不应指定 DSPRINT \_ 的操作发布。）

当函数收到打印机[**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent) \_ 事件 INITIALIZE 事件时，应在打印机驱动程序的 DrvPrinterEvent 函数中实现这些步骤 \_ 。

如果驱动程序必须获取打印机发布的属性的当前值，则它应调用**GetPrinterDataEx**或**EnumPrinterDataEx** ，以从注册表中获取信息，该信息为后台处理程序并始终处于最新状态。 另一种方法是调用**GetPrinter**以获取打印队列的对象标识符，然后调用 ADSI 函数以获取已发布属性的值。 不建议使用此方法，因为它会占用大量的资源，并且返回的数据可能并非总是最新的。

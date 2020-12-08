---
title: 打印机目录服务的打印机驱动程序支持
description: 打印机目录服务的打印机驱动程序支持
keywords:
- 目录服务 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a084b06c0d481f3253546103a9780b40c308725
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807309"
---
# <a name="printer-driver-support-for-printer-directory-services"></a>打印机目录服务的打印机驱动程序支持





打印机驱动程序不负责向目录服务发布打印队列。 Microsoft Windows 2000 和更高版本打印文件夹通过在安装打印机的过程中调用 **SetPrinter** 函数) 来创建打印队列对象 (。

将发布打印队列属性，以便用户可以使用任务栏的 "**开始**" 菜单上的 "**搜索**" 选项搜索具有特定属性的打印机。 打印文件夹发布了某些（但不是全部） DriverCapabilities 提供的打印机功能。 仅会发布被认为对浏览目的很有用的功能。

打印机驱动程序可以添加或修改打印队列对象的属性信息。 可发布的打印队列属性由 winspool.drv 中定义的 **SPLDS \_** 前缀常量标识。 若要添加或修改打印机属性，您的驱动程序必须使用这些预定义的属性名称标识符。

若要添加或修改打印队列对象的属性信息，请执行以下步骤：

1.  \_ \_ 通过调用后台处理程序的 **SetPrinterDataEx** 函数，将属性名称和值添加到注册表中的 SPLDS DRIVER 项下。

1.  调用后台处理程序的 **SetPrinter** 函数，其中包含打印机信息7的输入结构 \_ \_ (Windows SDK 文档中所述的) 和操作 "DSPRINT \_ 更新"，通知后台处理程序应更新已发布的打印队列对象。  (驱动程序不应指定 DSPRINT 发布的操作 \_ 。 ) 

当函数收到打印机 [**DrvPrinterEvent**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent) \_ 事件 INITIALIZE 事件时，应在打印机驱动程序的 DrvPrinterEvent 函数中实现这些步骤 \_ 。

如果驱动程序必须获取打印机发布的属性的当前值，则它应调用 **GetPrinterDataEx** 或 **EnumPrinterDataEx** ，以从注册表中获取信息，该信息为后台处理程序并始终处于最新状态。 另一种方法是调用 **GetPrinter** 以获取打印队列的对象标识符，然后调用 ADSI 函数以获取已发布属性的值。 不建议使用此方法，因为它会占用大量的资源，并且返回的数据可能并非总是最新的。

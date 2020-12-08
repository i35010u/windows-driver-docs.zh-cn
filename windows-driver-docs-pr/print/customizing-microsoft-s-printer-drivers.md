---
title: 自定义 Microsoft 打印机驱动程序
description: 自定义 Microsoft 打印机驱动程序
keywords:
- 打印机驱动程序自定义 WDK
- 自定义打印机驱动程序 WDK
- 打印机驱动程序自定义 WDK，关于自定义打印机驱动程序
- 自定义打印机驱动程序 WDK，关于自定义打印机驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34b5219a058afb6d6a9c30ffd5a3685c9e54b5ec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797375"
---
# <a name="customizing-microsoft-printer-drivers"></a>自定义 Microsoft 打印机驱动程序


[Microsoft 通用打印机驱动程序](microsoft-universal-printer-driver.md)的设计 (Unidrv) 和[Microsoft PostScript 打印机驱动程序](microsoft-postscript-printer-driver.md) (PSCRIPT) 基于基于 NT 的操作系统[打印机驱动程序体系结构](printer-driver-architecture.md)。 因此，每个组件都由两个组件组成：一个 [打印机接口 dll](printer-interface-dll.md) 和一个 [打印机图形 dll](printer-graphics-dll.md)。 本部分介绍如何自定义这些组件。

若要自定义为 Unidrv 或 Pscript 提供的打印机接口 DLL，必须提供一个或多个 [用户界面插件](user-interface-plug-ins.md)。您可以使用这些插件来修改驱动程序的用户界面，并为某些打印机事件提供额外的处理。 如果使用的是 Windows Vista 中的 Unidrv，则可以完全替换用户界面。

若要自定义为 Unidrv 或 Pscript 提供的打印机图形 DLL，必须提供一个或多个 [呈现插件](rendering-plug-ins.md)。您可以使用这些插件来修改发送到打印作业的数据流中的打印后台处理程序的数据。

本节包括下列主题：

[用户界面插件](user-interface-plug-ins.md)

[渲染插件](rendering-plug-ins.md)

[实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)

[安装自定义的驱动程序组件](installing-customized-driver-components.md)

[通用属性页用户界面](common-property-sheet-user-interface.md)

[打印机的颜色管理](color-management-for-printers.md)

[将打印票证支持添加到打印驱动程序](adding-print-ticket-support-to-print-drivers.md)

[文档设备的设备阶段](device-stage-for-document-devices.md)

 

 





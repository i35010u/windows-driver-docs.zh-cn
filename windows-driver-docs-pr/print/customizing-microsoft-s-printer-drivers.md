---
title: 自定义 Microsoft 打印机驱动程序
description: 自定义 Microsoft 打印机驱动程序
ms.assetid: b7761209-1f6f-4288-af47-4ed855c2e629
keywords:
- 自定义 WDK 的打印机驱动程序
- 自定义打印机驱动程序 WDK
- 自 WDK，定义有关自定义打印机驱动程序的打印机驱动程序
- 有关自定义打印机驱动程序的自定义打印机驱动程序 WDK，
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 361235638ddee507431f86d8d9f46f7dea86c9cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562817"
---
# <a name="customizing-microsoft-printer-drivers"></a>自定义 Microsoft 打印机驱动程序


设计[Microsoft 通用打印机驱动程序](microsoft-universal-printer-driver.md)(Unidrv) 和[Microsoft PostScript 打印机驱动程序](microsoft-postscript-printer-driver.md)(Pscript) 在基于 NT 的操作系统上基于[打印机驱动程序体系结构](printer-driver-architecture.md)。 因此，每个由两个组件组成-[打印机接口 DLL](printer-interface-dll.md)和一个[打印机图形 DLL](printer-graphics-dll.md)。 本部分介绍如何自定义这些组件。

若要自定义为 Unidrv 或 Pscript DLL 提供的打印机接口，必须提供一个或多个[用户界面插件](user-interface-plug-ins.md)。若要修改的驱动程序的用户界面并提供额外处理某些打印机的事件，可以使用这些插件。 如果使用的从 Windows Vista Unidrv，您可以完全替换用户界面。

若要自定义 DLL 为 Unidrv 或 Pscript 提供打印机图形，必须提供一个或多个[呈现插件](rendering-plug-ins.md)。这些插件可用于修改发送到打印作业的数据的流中的打印后台处理程序的数据。

本部分包括以下主题：

[用户界面插件](user-interface-plug-ins.md)

[呈现插件](rendering-plug-ins.md)

[实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)

[安装自定义驱动程序组件](installing-customized-driver-components.md)

[常用属性页用户界面](common-property-sheet-user-interface.md)

[打印机的颜色管理](color-management-for-printers.md)

[添加打印驱动程序的打印票证支持](adding-print-ticket-support-to-print-drivers.md)

[Device Stage 文档设备](device-stage-for-document-devices.md)

 

 





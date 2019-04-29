---
title: UI 插件的 COM 接口
description: UI 插件的 COM 接口
ms.assetid: 9cc6502b-a003-4d0b-857e-4653cf6fa0ea
keywords:
- 用户界面插件 WDK 打印，COM 接口
- UI 插件 WDK 打印，COM 接口
- COM 接口 WDK 打印，用户界面插件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf15ccce5b96267ded0dce6f0cd73e40c18f957a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383580"
---
# <a name="com-interfaces-for-ui-plug-ins"></a>UI 插件的 COM 接口





为 Microsoft 的打印机驱动程序和 UI 插件之间的通信定义以下 COM 接口：

-   [IPrintOemCommon COM 接口](iprintoemcommon-com-interface.md)，其中提供了指定和获取设备信息的方法。

-   [IPrintOemUI COM 接口](iprintoemui-com-interface.md)，它使[打印机接口 DLL](printer-interface-dll.md) Unidrv 或 Pscript5 调用 UI 插件。

-   [IPrintOemUI2 COM 接口](iprintoemui2-com-interface.md)，用于延长[IPrintOemUI COM 接口](iprintoemui-com-interface.md)。

-   [IPrintOemUIMXDC COM 接口](iprintoemuimxdc-com-interface.md)，这使 UI 插件来控制转换从 GDI 到 XPS 输出筛选器管道驱动程序中调用。

-   [IPrintOemDriverUI COM 接口](iprintoemdriverui-com-interface.md)，其提供给 UI 插件的实用程序操作。

-   [IPrintCoreUI2 COM 接口](iprintcoreui2-com-interface.md)，提供 UI 插件微型驱动程序的帮助器方法。

下图显示 UI 插件中使用的 COM 接口的继承树。

![说明在 ui 插件中使用的 com 接口的继承树关系图](images/uiintf2.png)

 

 





---
title: UI 插件的 COM 接口
description: UI 插件的 COM 接口
keywords:
- 用户界面插件 WDK 打印，COM 接口
- UI 插件 WDK 打印，COM 接口
- COM 接口 WDK 打印，用户界面插件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49b93fd52e411cd6d64db0ce61f6ffadc0f2f922
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797683"
---
# <a name="com-interfaces-for-ui-plug-ins"></a>UI 插件的 COM 接口





为 Microsoft 的打印机驱动程序和 UI 插件之间的通信定义了下列 COM 接口：

-   [IPRINTOEMCOMMON COM 接口](iprintoemcommon-com-interface.md)，用于提供指定和获取设备信息的方法。

-   [IPRINTOEMUI COM 接口](iprintoemui-com-interface.md)，该接口允许 Unidrv 或 Pscript5 的 [打印机接口 DLL](printer-interface-dll.md) 调用 UI 插件。

-   [IPRINTOEMUI2 com 接口](iprintoemui2-com-interface.md)，用于扩展 [IPrintOemUI com 接口](iprintoemui-com-interface.md)。

-   [IPRINTOEMUIMXDC COM 接口](iprintoemuimxdc-com-interface.md)，该接口使 UI 插件能够控制在筛选器管道驱动程序中从 GDI 调用到 XPS 输出的转换。

-   [IPRINTOEMDRIVERUI COM 接口](iprintoemdriverui-com-interface.md)，可为 UI 插件提供实用工具操作。

-   [IPRINTCOREUI2 COM 接口](iprintcoreui2-com-interface.md)，为微型驱动程序 UI 插件提供帮助器方法。

下图显示了在 UI 插件中使用的 COM 接口的继承树。

![阐释 ui 插件中使用的 com 接口的继承树的关系图](images/uiintf2.png)

 

 





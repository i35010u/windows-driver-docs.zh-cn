---
title: 渲染插件的 COM 接口
description: 渲染插件的 COM 接口
keywords:
- 呈现插件 WDK 打印，COM 接口
- COM 接口 WDK 打印，呈现插件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b3a9ea453b0e1d8c3695f72a4d07ea9b57cbe73
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797693"
---
# <a name="com-interfaces-for-rendering-plug-ins"></a>渲染插件的 COM 接口





为 Microsoft 的打印机驱动程序和呈现插件之间的通信定义了下列 COM 接口：

[IPRINTOEMUNI COM 接口](iprintoemuni-com-interface.md)，该接口允许 Unidrv 的 [打印机图形 DLL](printer-graphics-dll.md) 调用呈现插件。

[IPRINTOEMUNI2 Com 接口](iprintoemuni2-com-interface.md)，用于扩展 IPrintOemUni COM 接口的功能。

[IPRINTOEMUNI3 Com 接口](iprintoemuni3-com-interface.md)，用于扩展 IPrintOemUni 和 IPrintOemUni2 COM 接口的功能。

[IPRINTOEMDRIVERUNI COM 接口](iprintoemdriveruni-com-interface.md)，用于提供实用工具操作来呈现 Unidrv 的插件。

[IPRINTOEMPS COM 接口](iprintoemps-com-interface.md)，该接口允许 Pscript5 的 [打印机图形 DLL](printer-graphics-dll.md) 调用呈现插件。

[IPRINTOEMPS2 Com 接口](iprintoemps2-com-interface.md)，用于扩展 IPrintOemPS COM 接口的功能。

[IPRINTOEMDRIVERPS COM 接口](iprintoemdriverps-com-interface.md)，用于提供实用工具操作来呈现 Pscript5 的插件。

[IPRINTCOREPS2 COM 接口](iprintcoreps2-com-interface.md)，为 Pscript5 微型驱动程序呈现插件提供帮助器方法。

下图显示了用于呈现插件的 COM 接口的继承树。

![说明用于呈现插件的 com 接口的继承树的关系图](images/rendintf.png)

 

 





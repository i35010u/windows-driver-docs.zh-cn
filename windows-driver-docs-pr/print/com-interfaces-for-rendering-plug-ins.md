---
title: 用于呈现插件的 COM 接口
description: 用于呈现插件的 COM 接口
ms.assetid: 3a1a67ed-7c29-42fa-9bd2-ee38468f6d4b
keywords:
- 呈现插件 WDK 打印，COM 接口
- COM 接口 WDK 打印，呈现插件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b74e4b2af07f9c1479828842a9795629aec3899
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522712"
---
# <a name="com-interfaces-for-rendering-plug-ins"></a>用于呈现插件的 COM 接口





为 Microsoft 的打印机驱动程序和呈现插件之间的通信定义以下 COM 接口：

[IPrintOemUni COM 接口](iprintoemuni-com-interface.md)，它允许[打印机图形 DLL](printer-graphics-dll.md)为 Unidrv 调用呈现插件。

[IPrintOemUni2 COM 接口](iprintoemuni2-com-interface.md)，扩展了 IPrintOemUni COM 接口的功能。

[IPrintOemUni3 COM 接口](iprintoemuni3-com-interface.md)，扩展了 IPrintOemUni 的功能和 IPrintOemUni2 COM 接口。

[IPrintOemDriverUni COM 接口](iprintoemdriveruni-com-interface.md)，提供对呈现插件用于 Unidrv 的实用程序操作。

[IPrintOemPS COM 接口](iprintoemps-com-interface.md)，它允许[打印机图形 DLL](printer-graphics-dll.md)为 Pscript5 调用呈现插件。

[IPrintOemPS2 COM 接口](iprintoemps2-com-interface.md)，扩展了 IPrintOemPS COM 接口的功能。

[IPrintOemDriverPS COM 接口](iprintoemdriverps-com-interface.md)，提供对呈现插件用于 Pscript5 的实用程序操作。

[IPrintCorePS2 COM 接口](iprintcoreps2-com-interface.md)，其中提供了 Pscript5 微型驱动程序的帮助器方法呈现插件。

下图显示了呈现器插件中使用的 COM 接口的继承树。

![说明中使用的 com 接口的继承树关系图呈现插件](images/rendintf.png)

 

 





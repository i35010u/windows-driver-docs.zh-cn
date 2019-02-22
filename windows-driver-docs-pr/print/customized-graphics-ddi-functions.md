---
title: 自定义的图形 DDI 函数
description: 自定义的图形 DDI 函数
ms.assetid: 33d7d567-5371-4873-a4ef-cd2b06f65d73
keywords:
- 呈现插件 WDK 打印，图形 DDI 函数
- 图形 DDI 函数 WDK 打印
- 挂接图形 DDI 函数 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aeeeaeedfce98e2b4ef4eadbcfa271ee61bd19a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519994"
---
# <a name="customized-graphics-ddi-functions"></a>自定义的图形 DDI 函数





打印机微型驱动程序开发人员可以扩展功能的核心打印机驱动程序图形 DDIs 通过实现插件方法。 插件呈现可挂接出一些图形 DDI 功能，并提供核心打印机驱动程序函数的自定义的实现。 新打印机呈现插件的开发人员应实现其插件的基于 COM 的方法。请参阅[COM 接口的呈现插件](com-interfaces-for-rendering-plug-ins.md)有关一系列定义 COM 接口。

在 COM 接口的发布之前, Ihv 可以扩展图形 DDIs 的功能通过实现一个或多个 OEM*Xxx*其呈现插件的函数。尽管这些函数的用法仍支持出于兼容性原因，但新呈现插件的编写器应使用中的 COM 接口的方法。

本部分的剩余部分包含以下主题：

[基于 COM 的呈现插件](com-based-rendering-plug-ins.md)

[非基于 COM 的呈现插件](non-com-based-rendering-plug-ins.md)

 

 





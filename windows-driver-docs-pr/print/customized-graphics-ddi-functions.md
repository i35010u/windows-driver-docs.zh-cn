---
title: 自定义的图形 DDI 函数
description: 自定义的图形 DDI 函数
keywords:
- 呈现插件 WDK 打印，图形 DDI 函数
- 图形 DDI 函数 WDK 打印
- 挂钩图形 DDI 功能 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 970d5121266303ce7b8dd6ec3792f7d9cc00b84c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797405"
---
# <a name="customized-graphics-ddi-functions"></a>自定义的图形 DDI 函数





打印机微型驱动程序开发人员可以通过实现插件方法来扩展核心打印机驱动程序图形 DDIs 的功能。 呈现插件可以挂钩一些图形 DDI 函数，以提供核心打印机驱动程序函数的自定义实现。 新的打印机呈现插件开发人员应为插件实现基于 COM 的方法。有关定义的 COM 接口的列表，请参阅 [用于呈现插件的 COM 接口](com-interfaces-for-rendering-plug-ins.md) 。

在发布 COM 接口之前，Ihv 可以通过为其呈现插件实现一个或多个 OEM *Xxx* 函数来扩展图形 DDIs 的功能。尽管出于兼容性原因仍支持使用这些函数，但新的呈现插件的编写器应使用 COM 接口中的方法。

本部分的其余部分包含以下主题：

[基于 COM 的渲染插件](com-based-rendering-plug-ins.md)

[不是基于 COM 的渲染插件](non-com-based-rendering-plug-ins.md)

 

 





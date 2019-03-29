---
title: 什么是 Defaultwpp.ini 文件
description: 什么是 Defaultwpp.ini 文件
ms.assetid: 7e2673a3-5a01-498a-a2af-e5d8ff3e088b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9fdefbd78b6e6c5c4593cc0633b9168e8a0edef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565590"
---
# <a name="what-is-the-defaultwppini-file"></a>什么是 Defaultwpp.ini 文件？


Defaultwpp.ini 文件是定义的数据类型的支持软件跟踪配置文件。 Defaultwpp.ini 文件位于 bin\\wppconfig\\rev1 子目录的 Windows Driver Kit (WDK)。

Defaultwpp.ini 文件包括以下组件：

-   算术数据类型，如 UBYTE 和 XINT64

-   依赖于体系结构的数据类型，例如 SLONGPTR

-   预定义的常量-COMPNAME （计算机名称），如 %！FUNC ！ （函数名称） 和 %！级别 ！ （提供程序级别--），将其纳入[跟踪消息前缀](trace-message-prefix.md)通过编辑 %跟踪\_格式\_前缀 %环境变量

-   格式规范常量，可在使用中的跟踪消息中使用格式规范**printf**语句。

-   常用于跟踪，如 IPADDR、 HRESULT 和 GUID 类型的特殊类型。

-   与时间相关的类型，如日期、 时间戳，仍未付款和差异。

-   枚举类型，如 b1 （8 个字节的集） 和布尔值 (Boolean)。

-   自定义类型，如 irql、 pnpmn 和 sysctrl。

您可以在 Defaultwpp.ini 文件中使用的数据类型和创建自己的自定义配置文件具有简单和复杂数据类型。 有关详细信息，请参阅[如何定义自定义数据类型？](how-do-you-define-custom-data-types-.md)并[什么是复杂的语法类型定义？](what-is-the-syntax-of-the-complex-types-definition-.md)。

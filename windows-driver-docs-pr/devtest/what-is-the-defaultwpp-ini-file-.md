---
title: 什么是 Defaultwpp.ini 文件
description: 什么是 Defaultwpp.ini 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcb8483cfae96b8addf9b23514674a3cc2df758e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810711"
---
# <a name="what-is-the-defaultwppini-file"></a>什么是 Defaultwpp.ini 文件？


Defaultwpp.ini 文件是定义支持软件跟踪的数据类型的配置文件。 Defaultwpp.ini 文件位于 \\ \\ Windows 驱动程序工具包 (WDK) 的 bin wppconfig 4.1 子目录中。

Defaultwpp.ini 文件包括以下内容：

-   算术数据类型，如 UBYTE 和 XINT64

-   与体系结构相关的数据类型，例如 SLONGPTR

-   预定义的常量-例如，COMPNAME (计算机名) ，%！求!  (函数名称) 和%！调配!  (提供程序级别) -可以通过编辑% TRACE [trace message prefix](trace-message-prefix.md) \_ 格式 \_ 前缀% 环境变量，将其包含在跟踪消息前缀中

-   格式规范常量，使你能够在跟踪消息中使用格式规范，就像在 **printf** 语句中使用的一样。

-   通常在跟踪中使用的类型的特殊类型，如 IPADDR、HRESULT 和 GUID。

-   与时间有关的类型，例如日期、时间戳、截止日期和增量类型。

-   枚举类型，例如 b1 (8 字节的集合) 和布尔值 (布尔) 。

-   自定义类型（如 irql、pnpmn 和 sysctrl）。

您可以使用 Defaultwpp.ini 文件中的数据类型，并创建自己的自定义配置文件，该文件具有简单和复杂的数据类型。 有关详细信息，请参阅 [如何定义自定义数据类型？](how-do-you-define-custom-data-types-.md) 和 [复杂类型定义的语法是什么？](what-is-the-syntax-of-the-complex-types-definition-.md)。

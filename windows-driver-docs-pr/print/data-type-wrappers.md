---
title: 数据类型包装器
description: 数据类型包装器
keywords:
- 快照 WDK GDL，结构
- GDL WDK，枚举
- 枚举 WDK GDL
- 数据类型 WDK GDL
- GDL WDK，数据类型
- 分析器 WDK GDL，数据类型包装器
- 快照 WDK GDL，数据类型 wrapers
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3a32b427552bbe92c0b2122d44a224761f07951
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797341"
---
# <a name="data-type-wrappers"></a>数据类型包装器


GDL 分析器将每个模板定义的数据类型包装在另一种数据类型中，该数据类型包含可能出现在实际快照中的 XML 特性的适当声明。 这种额外的数据类型是必需的，因为 XSD 架构会将元素开始标记中显示的未声明的 XML 属性视为架构验证错误。 另外，这种额外的数据类型还无需知道分析器在内部使用的特性，并使模板不受快照中将来更改的隔离。

 

 





---
title: 数据类型包装器
description: 数据类型包装器
ms.assetid: 8c88002b-4d0a-4e81-b50d-f765caa7cf80
keywords:
- 快照 WDK GDL，结构
- GDL WDK 枚举
- 枚举 WDK GDL
- 数据类型 WDK GDL
- GDL WDK，数据类型
- 分析器 WDK GDL，数据类型的包装
- 快照 WDK GDL，数据类型 wrapers
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cea285f931f3f5c7ac190fea891e102af3eca303
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341301"
---
# <a name="data-type-wrappers"></a>数据类型包装器


GDL 分析器将每个模板定义的数据类型包装在另一个数据类型，包含可能在实际的快照中显示的 XML 特性的适当声明。 需要此额外的数据类型，因为 XSD 架构将视为未声明出现在元素开始标记作为架构验证错误的 XML 特性。 此额外的数据类型也不需要您知道由分析器在内部使用的属性，并隔离从快照中的未来更改的模板。

 

 





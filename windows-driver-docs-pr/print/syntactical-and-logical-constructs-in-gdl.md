---
title: 中 GDL 语法和逻辑的构造
description: 中 GDL 语法和逻辑的构造
ms.assetid: f0802424-319c-4ba4-a8cd-539006f4d22c
keywords:
- 语法构造 WDK GDL
- 逻辑构造 WDK GDL
- 构造 WDK GDL，语法构造
- 构造 WDK GDL，逻辑构造
- GDL WDK 构造
- 分析器 WDK GDL，处理构造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a55f040b9df1aaa885a9a56ac90d8830d913371
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543572"
---
# <a name="syntactical-and-logical-constructs-in-gdl"></a>中 GDL 语法和逻辑的构造


GDL 区分按原义由 GDL 源代码文件中的项定义的构造和 GDL 的内部数据中的这些构造的表示形式。 前者是语法表示形式，后者是逻辑表示形式。 表示形式不同源文件中定义的构造时。 GDL 分析器创建只有一个逻辑表示形式为给定的构造类型和构造标记，无论多少次 GDL 源代码文件中定义此类构造的构造。

 

 





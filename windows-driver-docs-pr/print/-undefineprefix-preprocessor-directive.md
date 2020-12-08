---
title: '#UndefinePrefix 预处理器指令'
description: '#UndefinePrefix 预处理器指令'
keywords:
- 预处理器指令 WDK GDL，关键字
- 关键字 WDK GDL
- 保留关键字 WDK
- UndefinePrefix 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d8fd391010723b247a2479b29a5b2c97ec7a1d9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812435"
---
# <a name="undefineprefix-preprocessor-directive"></a>\#UndefinePrefix 预处理器指令


```GDL
#UndefinePrefix:
```

\#UndefinePrefix 指令删除当前前缀。 之前定义的前缀将成为当前前缀。 仅可定义使用[ \# SetPPPrefix](-setppprefix-preprocessor-directive.md)指令定义的前缀。 不能定义系统默认前缀。 此指令不使用符号。

此预处理器前缀是 GDL 的新前缀。

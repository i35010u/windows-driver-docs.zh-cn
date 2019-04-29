---
title: '#UndefinePrefix 预处理器指令'
description: '#UndefinePrefix 预处理器指令'
ms.assetid: 7c99c2cf-6609-4fec-ae21-1477699ba5c8
keywords:
- 预处理器指令 WDK GDL，关键字
- 关键字 WDK GDL
- 保留的关键字 WDK
- UndefinePrefix 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82adc4b5554b15f883f8e728cfbc1f9664cfa693
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372914"
---
# <a name="undefineprefix-preprocessor-directive"></a>\#UndefinePrefix 预处理器指令


```GDL
#UndefinePrefix:
```

\#UndefinePrefix 指令将删除当前的前缀。 以前定义的前缀将成为当前的前缀。 通过使用定义的前缀[ \#SetPPPrefix](-setppprefix-preprocessor-directive.md)指令可以是未定义。 系统默认的前缀不能为未定义。 此指令不使用符号。

此预处理器的前缀是 GDL 的新增功能。

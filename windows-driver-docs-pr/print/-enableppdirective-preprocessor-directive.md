---
title: '#EnablePPDirective 预处理器指令'
description: '#EnablePPDirective 预处理器指令'
keywords:
- 预处理器指令 WDK GDL，关键字
- 关键字 WDK GDL
- 保留关键字 WDK
- EnablePPDirective 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 146dec5989be6c1868fb79307315bba12e656399
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794277"
---
# <a name="enableppdirective-preprocessor-directive"></a>\#EnablePPDirective 预处理器指令


```GDL
#EnablePPDirective: Directive
```

\#EnablePPDirective 允许启用已禁用的指令。 未来版本的 GDL 分析器可能会定义其他预处理器指令。 如果现有的 GDL 文件也将新的指令名称用于其自身用途，则在新的分析器上分析现有的 GDL 文件可能会产生意外的结果。 若要避免这种向前兼容性问题，则默认情况下将禁用任何新指令，并需要使用 \# EnablePPDirective 指令启用。 *指令* 值是在没有任何前缀) 的情况下启用 (指令的基名称。 指令名称是必需的值。

此预处理器指令是 GDL 的新指令。

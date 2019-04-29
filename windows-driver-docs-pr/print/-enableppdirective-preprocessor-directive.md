---
title: '#EnablePPDirective 预处理器指令'
description: '#EnablePPDirective 预处理器指令'
ms.assetid: aebb11ec-b281-461e-b3fd-65e9b2773049
keywords:
- 预处理器指令 WDK GDL，关键字
- 关键字 WDK GDL
- 保留的关键字 WDK
- EnablePPDirective 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1605a374a3fb3165f9909cc0d707c61956c3b6e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383576"
---
# <a name="enableppdirective-preprocessor-directive"></a>\#EnablePPDirective 预处理器指令


```GDL
#EnablePPDirective: Directive
```

\#EnablePPDirective 允许已禁用的指令来启用。 GDL 分析器的未来版本可能会定义其他预处理器指令。 如果现有 GDL 文件还具有使用该新指令名称来根据自己的需要，分析现有 GDL 文件可能具有在新的分析器的意外的结果。 若要避免此向前兼容性问题，任何新指令将默认情况下禁用，并且将需要使用启用\#EnablePPDirective 指令。 *指令*值是启用 （不带任何前缀） 的指令的基名称。 指令的名称是必需的值。

此预处理器指令是 GDL 的新增功能。

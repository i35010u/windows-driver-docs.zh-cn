---
title: GDL 预处理器语法
description: GDL 预处理器语法
ms.assetid: 14e9a595-3b6f-43b9-b670-7c9324619974
keywords:
- 指令 WDK GDL，源文件预处理器指令
- 源文件 WDK GDL，预处理器指令
- 预处理器指令 WDK GDL，语法
- 语法 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a14013167d268811f74bbb8051f24e5152dcb7d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380010"
---
# <a name="gdl-preprocessor-syntax"></a>GDL 预处理器语法


GDL 预处理器指令必须遵守以下规则：

-   所有预处理器指令必须占用一个单独的行，并且必须是该行的唯一语句。 可选空格仅可以在预处理器指令之前。 在同一行中按照指令任何无关字符会删除之前将文件提交到的分析的第二个 （主要） 阶段。

-   所有指令必须具有当前的预处理器前缀作为都前缀。 预处理器的前缀值最初设置为星号分析器 (\*) 或数字符号 (\#)，但您可以通过使用前缀更改为任何字符或令牌 **\#SetPPPrefix**指令。

-   若要被识别为预处理器指令，预处理器的前缀必须紧跟在指令，和如果指令需要值，必须用冒号 （:） 分隔值。

-   由任何空格或 linebreak 字符终止指令的值。

**请注意**   GDL 语法是比 GPD 语法相对较为宽松。 如果要为这两个分析器编写，则应遵循的更严格的语法所需的 GPD。

 

 

 





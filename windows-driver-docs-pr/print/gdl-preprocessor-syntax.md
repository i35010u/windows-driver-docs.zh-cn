---
title: GDL 预处理器语法
description: GDL 预处理器语法
keywords:
- 指令 WDK GDL，源文件预处理器指令
- 源文件 WDK GDL，预处理器指令
- 预处理器指令 WDK GDL，语法
- 语法 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a33efca760cd32483308c5b857742ede991305d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796967"
---
# <a name="gdl-preprocessor-syntax"></a>GDL 预处理器语法


GDL 预处理器指令必须遵循以下规则：

-   所有预处理器指令必须占用单独的行，并且必须是该行的唯一语句。 预处理器指令之前只有可选的空白。 在将文件提交到第二个 (主) 分析阶段之前，将删除在同一行上遵循指令的任何外来字符。

-   所有指令必须以当前预处理器前缀为前缀。 预处理器前缀最初由分析器设置为星号 (\*) 或数字符号 (\#) ，但你可以使用 **\# SetPPPrefix** 指令将前缀更改为任意字符或令牌。

-   若要识别为预处理器指令，预处理器前缀必须紧跟在指令后，如果指令需要值，则必须用冒号分隔该值 (： ) 。

-   指令的值由任何空格或 linebreak 字符终止。

**注意**   GDL 语法比 GPD 语法更宽松。 如果要为两个分析器编写，应遵循 GPD 所需的更严格语法。

 

 

 





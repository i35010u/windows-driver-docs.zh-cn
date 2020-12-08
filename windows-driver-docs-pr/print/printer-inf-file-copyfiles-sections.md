---
title: 打印机 INF 文件的 CopyFiles 节
description: 打印机 INF 文件的 CopyFiles 节
keywords:
- INF 文件 WDK print，CopyFiles 部分
- 部分 WDK 打印机
- CopyFiles 指令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f57ada5109b0b3eb640352391ae760471f7ddfc3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807275"
---
# <a name="printer-inf-file-copyfiles-sections"></a>打印机 INF 文件的 CopyFiles 节





如果打印机 INF 文件包含由 [**INF CopyFiles 指令**](../install/inf-copyfiles-directive.md)引用的文件列表部分，则必须使用以下格式指定文件列表中的每个文件：

**\[**<em>文件列表部分</em> **\]** 
*目标-文件名， \[ ，标志 \]* 
 *目标-文件名 \[ ，，标志 \]* 
 *目标-文件名 \[ ，，标志 \]* .。。"*目标文件名*" 字段是必填字段，"*标志*" 字段是可选的。 文件规范不能包含为与 INF CopyFiles 指令一起使用的文件列表部分定义的可选的 *源文件名* 或 *临时文件名* 字段。 此限制是从网页安装打印驱动程序所必需的。

 


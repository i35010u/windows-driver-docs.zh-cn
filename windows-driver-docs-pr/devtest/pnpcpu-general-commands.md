---
title: PNPCPU 常规命令
description: PNPCPU 常规命令
keywords:
- PNPCPU WDK，命令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac6b1768028caad0150d37098eed786488fbb12e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841043"
---
# <a name="pnpcpu-general-commands"></a>PNPCPU 常规命令


以下语法适用于所有 PNPCPU 操作。

```
pnpcpu.exe -operation
```

### <a name="span-idparametersspanspan-idparametersspanparameters"></a><span id="parameters"></span><span id="PARAMETERS"></span>参数

<span id="-install"></span><span id="-INSTALL"></span>**-install**  
在本地计算机上安装该工具。

<span id="-uninstall"></span><span id="-UNINSTALL"></span>**-卸载**  
从本地计算机中删除该工具，并将计算机恢复 **为运行前的状态**。

这包括清除运行 **安装** 命令后可能观察到的所有处理器错误代码，并重新启动系统。

<span id="-add"></span><span id="-ADD"></span>**-添加**  
在系统中的每个逻辑处理器上执行热添加操作，最高可达许可的最大支持。

<span id="-__or_-help"></span><span id="-__OR_-HELP"></span>**-?** 或 **-help**  
显示类似于此文档的使用情况信息。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

对于列出的任何命令，没有其他可选参数。

 

 






---
title: .browse（在浏览器中显示命令）
description: Browse 命令在新的命令浏览器窗口中显示指定命令的输出。
keywords:
- 。在浏览器中浏览 (显示命令) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .browse (Display Command in Browser)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 44f528f3b88d4ed0f5271342715f8f589c51483b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799953"
---
# <a name="browse-display-command-in-browser"></a>.browse（在浏览器中显示命令）


**Browse** 命令在新的 [命令浏览器窗口](command-browser-window.md)中显示指定命令的输出。

```dbgcmd
.browse Command
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="Command"></span><span id="command"></span><span id="COMMAND"></span>*Command*  
要执行并在新的命令浏览器窗口中显示的命令。

<a name="remarks"></a>备注
-------

下面的示例使用 .browser **命令在** 命令浏览器窗口中显示 [**链式/d**](-chain--list-debugger-extensions-.md) 命令的输出。

```dbgcmd
.browse .chain /D
```

 

 






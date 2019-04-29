---
title: 调试包含 JScript 帧的堆栈跟踪
description: JScript 堆栈转储创建和使用功能工作原理是收集 JScript 帧和拼接它们针对调试器物理帧。
ms.assetid: A470809F-55AA-4A49-B181-EC8D22C84F31
keywords:
- JScript
- jscript9diagdump.dll
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bdcca140685e6173392cd5fecc5ba0e60fd7621
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324555"
---
# <a name="debugging-a-stack-trace-that-has-jscript-frames"></a>调试包含 JScript 帧的堆栈跟踪


JScript 堆栈转储创建和使用功能工作原理是收集 JScript 帧和拼接它们针对调试器物理帧。 有时在 x86 平台、 堆栈跟踪不正确的调试器构造。

如果您的堆栈中包含您认为可能会不正确的 JScript 帧，则在调试器中输入以下命令。

**.stkwalk\_force\_frame\_pointer 1**

 

 






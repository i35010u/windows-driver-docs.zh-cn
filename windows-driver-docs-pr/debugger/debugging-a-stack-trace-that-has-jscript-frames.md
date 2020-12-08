---
title: 调试包含 JScript 帧的堆栈跟踪
description: JScript 堆栈转储的创建和使用功能的工作原理是收集 JScript 帧并将其与调试器物理帧一起使用。
keywords:
- JScript
- jscript9diagdump.dll
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8590412c6c75d14a4f4da85f3ed5fc07dcfc93a9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816389"
---
# <a name="debugging-a-stack-trace-that-has-jscript-frames"></a>调试包含 JScript 帧的堆栈跟踪


JScript 堆栈转储的创建和使用功能的工作原理是收集 JScript 帧并将其与调试器物理帧一起使用。 有时，在 x86 平台上，调试器不会正确地构造堆栈跟踪。

如果堆栈包含你认为可能不正确的 JScript 帧，请在调试器中输入以下命令。

**。 stkwalk \_ 强制 \_ 帧 \_ 指针1**

 

 






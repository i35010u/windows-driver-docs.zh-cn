---
title: 在 KD 中查看调用堆栈
description: 在 KD 中，可以通过输入其中一个 k (显示堆栈 Backtrace) 命令来查看调用堆栈。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e76633692ba64f58afa455fe4103c55133f6ec9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802873"
---
# <a name="viewing-the-call-stack-in-kd"></a>在 KD 中查看调用堆栈


调用堆栈是已导致程序计数器当前位置的函数调用的链。 调用堆栈上的 top 函数是当前函数，下一个函数是调用当前函数的函数，依此类推。 显示的调用堆栈基于当前程序计数器，除非更改寄存器上下文。 有关如何更改注册上下文的详细信息，请参阅 [更改上下文](changing-contexts.md)。

在 KD 中，可以通过输入其中一个 [**k (显示堆栈 Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令来查看调用堆栈。

 

 






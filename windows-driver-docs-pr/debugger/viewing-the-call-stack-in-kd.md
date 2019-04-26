---
title: 在 KD 中查看调用堆栈
description: 在 KD，可以通过输入一个 k （显示堆栈回溯） 命令来查看调用堆栈。
ms.assetid: 81F5D9EA-48CE-4F29-B74E-282824E690F6
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6793772ad6c0ff6ea65eb5e2d0f2322a491473ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325911"
---
# <a name="viewing-the-call-stack-in-kd"></a>在 KD 中查看调用堆栈


调用堆栈是导致程序计数器当前位置的函数调用链。 顶级函数在调用堆栈是当前函数下, 一个函数调用当前函数的函数，等等。 调用堆栈显示基于当前的程序计数器，除非您更改寄存器上下文。 有关如何更改寄存器上下文的详细信息，请参阅[更改上下文](changing-contexts.md)。

在 KD，可以查看调用堆栈，通过输入之一[ **k （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令。

 

 






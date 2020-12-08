---
title: C28602
description: 警告 C28602 避免在 HWND_BROADCAST 中调用 SendMessageTimeout。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28602
ms.openlocfilehash: 26c9ff19278530e0d46ebf4d02c54010ce8c5fa5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799781"
---
# <a name="c28602"></a>C28602


警告 C28602：避免通过 HWND 广播调用 SendMessageTimeout \_

当应用程序使用 **SendMessageTimeout** 时，代码分析工具将报告此警告，即使应用程序只请求10秒钟线程的超时期限。 在每个窗口超时之前，函数不会返回。应用程序在每个窗口响应所用的时间长度时，实际上可能会被阻止。 这是因为不能控制系统上每个其他 **HWND** 的响应时间。

若要解决此问题，请考虑改用 **PostMessage** ，使其不是阻止调用。 或者，避免使用 **HWND \_ 广播** 将消息定向到特定窗口。

 

 






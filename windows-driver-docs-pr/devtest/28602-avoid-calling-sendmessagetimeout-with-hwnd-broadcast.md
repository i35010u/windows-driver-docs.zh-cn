---
title: C28602
description: 警告 C28602 避免使用 HWND_BROADCAST 调用 SendMessageTimeout。
ms.assetid: 511df04e-97dc-43a2-9c48-ea1ffe62b813
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28602
ms.openlocfilehash: a2f1f0411acf48ff50e4366b4145822019e686aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569192"
---
# <a name="c28602"></a>C28602


警告 C28602:避免使用 HWND 调用 SendMessageTimeout\_广播

代码分析工具将报告此警告，当应用程序使用**SendMessageTimeout**，即使应用程序请求仅 10 秒的线程的超时期限。 该函数不返回之前每个窗口已超时。所响应的每个窗口的时间长度可能实际阻止应用程序。 这是因为它不是，可以控制的其他所有的响应时间**HWND**系统上。

若要解决此问题，请考虑使用**PostMessage**相反，因此它不是阻止调用。 或者，避免使用**HWND\_广播**将定向到特定的窗口消息。

 

 






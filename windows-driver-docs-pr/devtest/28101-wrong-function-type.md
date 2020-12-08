---
title: C28101
description: 警告 C28101 驱动程序模块已推断出当前函数不是正确的函数类型。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 05/01/2020
ms.localizationpriority: medium
f1_keywords:
- C28101
ms.openlocfilehash: 4adb789027ed94db901bf7fac182c846ffd9d69b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837819"
---
# <a name="c28101"></a>C28101


警告 C28101：驱动程序模块已推断当前函数不是正确的函数类型

代码分析工具检测到某个函数属于特定类型，如回调函数。 这只是一条信息性消息。 它不表示错误。

此消息指示代码分析工具正在应用特定于该函数类型的规则。 如果此推理错误，代码分析工具将生成误报警告，但可以安全地忽略这些警告。 有关详细信息，请参阅 [使用批注减少 C/c + + 代码缺陷](/cpp/code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects)。

*函数签名* (参数和结果类型) 用于尽可能地标识函数。 某些标准驱动程序例程（如 [**Cancel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel) 和 [**StartIo**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)）具有相同的签名，因此检查名称以查看它是否与该函数的传统名称匹配。 可能会检查传统名称的其他功能。

若要在它是冗余的情况下禁止显示此警告，可以显式声明函数为特定的函数类型。 通过这种方式检测到的函数通常是回调函数。 适当的操作是使用函数 typedef 声明它们。 有关详细信息，请参阅 [使用函数角色类型声明](using-function-role-type-declarations.md)。

 


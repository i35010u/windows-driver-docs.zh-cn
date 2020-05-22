---
title: C28101
description: 警告 C28101 驱动程序模块已推断出当前函数不是正确的函数类型。
ms.assetid: 81a68dd6-ff9d-4cb2-9bd9-3a0f0d152230
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 05/01/2020
ms.localizationpriority: medium
f1_keywords:
- C28101
ms.openlocfilehash: 842639441ff871dca82666080c4b3f28a08de6ad
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769461"
---
# <a name="c28101"></a>C28101


警告 C28101：驱动程序模块已推断当前函数不是正确的函数类型

代码分析工具检测到某个函数属于特定类型，如回调函数。 这只是一条信息性消息。 它不表示错误。

此消息指示代码分析工具正在应用特定于该函数类型的规则。 如果此推理错误，代码分析工具将生成误报警告，但可以安全地忽略这些警告。 有关详细信息，请参阅[使用批注减少 C/c + + 代码缺陷](https://docs.microsoft.com/cpp/code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects)。

*函数签名*（参数和结果类型）用于在可能时标识函数。 某些标准驱动程序例程（如[**Cancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)和[**StartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)）具有相同的签名，因此检查名称以查看它是否与该函数的传统名称匹配。 可能会检查传统名称的其他功能。

若要在它是冗余的情况下禁止显示此警告，可以显式声明函数为特定的函数类型。 通过这种方式检测到的函数通常是回调函数。 适当的操作是使用函数 typedef 声明它们。 有关详细信息，请参阅[使用函数角色类型声明](using-function-role-type-declarations.md)。

 

 






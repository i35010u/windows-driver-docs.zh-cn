---
title: C28101
description: 警告 C28101 驱动程序模块已推断当前函数不是正确的函数类型。
ms.assetid: 81a68dd6-ff9d-4cb2-9bd9-3a0f0d152230
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28101
ms.openlocfilehash: 52258c506cf53a14fb84f8e4b5a9941c00262b23
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364161"
---
# <a name="c28101"></a>C28101


警告 C28101:驱动程序模块已推断当前函数不是正确的函数类型

代码分析工具检测到的函数为特定类型，例如回调函数。 这只是一条信息性消息。 它不指示错误。

此消息指示代码分析工具应用特定于该函数类型的规则。 如果此推断出现错误，代码分析工具会生成误报警告，但可以安全地忽略这些警告。 有关详细信息，请参阅[使用注释减少 C /C++代码缺陷](https://go.microsoft.com/fwlink/p/?linkid=227826)。

*函数签名*（参数和结果类型） 用于标识应尽可能的函数。 一些标准驱动程序例程，如[**取消**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)并[ **StartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)，因此名称检查以查看是否具有相同的签名，它与该函数的常规名称相匹配。 其他函数可能会检查有约定俗成的名称。

若要禁止显示此警告，冗余时，可以显式声明为特定函数类型的函数。 检测到这种方式的函数通常是回调函数。 适当的操作是将它们使用的函数 typedef 声明。 有关详细信息，请参阅[使用函数角色类型声明](using-function-role-type-declarations.md)。

 

 






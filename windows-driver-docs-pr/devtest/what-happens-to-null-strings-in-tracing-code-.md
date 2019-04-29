---
title: 跟踪代码中的 NULL 字符串会发生什么情况
description: 跟踪代码中的 NULL 字符串会发生什么情况
ms.assetid: a2226cbd-28cf-48eb-b129-5c4d12eb2564
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07a917abc0a5ebbf24b6cc6883ad523bee12ada7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386387"
---
# <a name="what-happens-to-null-strings-in-tracing-code"></a>跟踪代码中的 NULL 字符串会发生什么情况？


默认情况下，在此版本的 Windows Driver Kit (WDK) 中的跟踪组件搜索**NULL**函数中传递的参数中的字符串。 因此，不需要验证每个自变量，以防止**NULL**中引发异常的字符串。

在早期版本的 WDK WPP\_检查\_有关\_NULL\_字符串宏执行此函数。 如果使用此版本的 WDK 生成内核模式驱动程序或用户模式应用程序，则可以从你的源代码中删除宏。

 

 






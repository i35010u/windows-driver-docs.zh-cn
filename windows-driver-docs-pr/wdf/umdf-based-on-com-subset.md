---
title: 基于 COM 子集的 UMDF
description: 基于 COM 子集的 UMDF
ms.assetid: 918459a9-a6a2-40b8-8b97-3aabe3e49bfb
keywords:
- UMDF 对象 WDK、 COM 子集
- framework 对象 WDK UMDF，COM 子集
- COM WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1aef0031d9c1c71b255a185cb2c648993b33fa15
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68229650"
---
# <a name="umdf-based-on-com-subset"></a>基于 COM 子集的 UMDF


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

由于以下原因，framework 对象和接口基于组件对象模型 (COM) 上：

-   COM 是许多应用程序程序员所熟悉的。

-   C++是用于 COM 应用程序编程的首选的语言。

-   COM 接口启用函数的逻辑分组，以便设备驱动程序接口 (DDI) 是易于理解和导航。

-   通过使用 COM，DDI 来扩展和发展而无需现有驱动程序要重新编译的 Dll。

-   大量的工具，包括 Microsoft Visual Studio 和活动模板库 (ATL) 支持基于 COM 的应用程序和对象。

框架将使用只有 COM; 一小部分它不依赖于整个 COM 基础结构和运行时库。 相反，框架将使用的查询接口和引用计数功能。 每个框架接口派生**IUnknown** ，并因此支持**QueryInterface**， **AddRef**，并**版本**方法默认情况下。 **AddRef**并**发行**方法管理对象生存期。 **QueryInterface**方法使其他组件可以决定将驱动程序支持哪些接口。

 

 






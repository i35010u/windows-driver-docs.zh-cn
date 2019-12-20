---
title: 基于 COM 子集的 UMDF
description: 基于 COM 子集的 UMDF
ms.assetid: 918459a9-a6a2-40b8-8b97-3aabe3e49bfb
keywords:
- UMDF 对象 WDK，COM 子集
- framework 对象 WDK UMDF，COM 子集
- COM WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a55744eb6acd64f800751fd610cd922f84b39c5b
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210255"
---
# <a name="umdf-based-on-com-subset"></a>基于 COM 子集的 UMDF


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

框架对象和接口基于组件对象模型（COM），原因如下：

-   许多应用程序程序员都对 COM 非常熟悉。

-   C++是用于编程 COM 应用程序的首选语言。

-   COM 接口启用函数的逻辑分组，以便设备驱动程序接口（DDI）易于理解和导航。

-   使用 COM 可以使 DDI 扩展和演化，而无需重新编译现有的驱动程序 Dll。

-   许多工具（包括 Microsoft Visual Studio 和活动模板库（ATL））都支持基于 COM 的应用程序和对象。

框架只使用 COM 的一小部分;它不依赖于整个 COM 基础结构和运行库。 相反，框架只使用查询接口和引用计数功能。 每个框架接口均派生自**IUnknown** ，因此默认情况下支持**QueryInterface**、 **AddRef**和**Release**方法。 **AddRef**和**Release**方法管理对象生存期。 **QueryInterface**方法使其他组件能够确定驱动程序支持的接口。

 

 






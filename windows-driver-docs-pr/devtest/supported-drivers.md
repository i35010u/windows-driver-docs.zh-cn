---
title: 支持的驱动程序
description: 支持的驱动程序
ms.assetid: 1d41a9a9-415a-4dba-8b52-138c47ad63fd
keywords:
- 静态驱动程序验证程序 WDK 要求
- StaticDV WDK 要求
- SDV WDK 要求
- 函数原型 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78811c4e2c1546efe7dc5f9feccfaec884c1102d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347658"
---
# <a name="supported-drivers"></a>支持的驱动程序


SDV 可以验证驱动程序，它必须能够解释的驱动程序代码，具体而言，驱动程序的入口点和函数以及支持的例程中的代码所需的驱动程序的功能。

以下部分介绍有关驱动程序和 SDV 要求驱动程序，它将验证的特定语法的基本要求。 SDV 不验证驱动程序符合这些要求，但如果驱动程序不符合，SDV 可能无法运行并且，在极少数情况下，它将报告 false 正或假负结果由于错误解释。

### <a name="span-idbasicdrivercharacteristicsspanspan-idbasicdrivercharacteristicsspanbasic-driver-characteristics"></a><span id="basic_driver_characteristics"></span><span id="BASIC_DRIVER_CHARACTERISTICS"></span>基本的驱动程序特征

SDV 是能够验证驱动程序具有以下特征：

-   SDV 验证驱动程序和用 C 编写的库和C++。

-   SDV 仅在符合 KMDF 和 WDM 符合设备驱动程序 （函数驱动程序、 筛选器驱动程序和总线驱动程序）、 NDIS 驱动程序 （筛选器、 微型端口和协议驱动程序） 和 Storport 驱动程序上执行完全验证。

-   SDV 尝试进行有限的泛型属性的验证 (如[NullCheck](nullcheckw.md)) 上不适合上述类别的驱动程序。

-   SDV 可以验证通过使用 WDM 函数角色类型来声明其驱动程序回调函数的 WDM 驱动程序。 有关如何声明函数的信息，请参阅[声明函数使用函数角色类型用于 WDM 驱动程序](declaring-functions-using-function-role-types-for-wdm-drivers.md)。

-   SDV 可以验证驱动程序时生成[内核模式驱动程序框架](https://msdn.microsoft.com/library/windows/hardware/ff544296)，前提是使用 SDV KMDF 回调函数角色类型声明的每个回调函数。 有关详细信息，请参阅[KMDF 驱动程序中使用函数角色类型声明函数](static-driver-verifier-kmdf-function-declarations.md)。

-   SDV 可以验证的 NDIS 驱动程序，提供通过使用 SDV NDIS 回调函数类型批注与函数声明每个回调函数。 有关详细信息，请参阅[NDIS 驱动程序中使用函数角色类型声明函数](static-driver-verifier-ndis-function-declarations.md)。

-   SDV 可以验证 Storport 驱动程序，前提是批注与函数声明每个回调函数。 通过使用 SDV Storport 回调函数类型执行此操作。 有关详细信息，请参阅[Storport 驱动程序中使用函数角色类型声明函数](declaring-functions-by-using-function-role-types-for-storport-drivers.md)。

### <a name="span-idbasicdriverrequirementsspanspan-idbasicdriverrequirementsspanbasic-driver-requirements"></a><span id="basic_driver_requirements"></span><span id="BASIC_DRIVER_REQUIREMENTS"></span>基本驱动程序要求

若要验证 WDM 驱动程序的 SDV，为驱动程序必须：

- 包括 wdm.h 中或 Ntddk.h （wdm.h 中是 Ntddk.h 的子集）。

- 使用中所述的方法创建设备对象[WDM 设备对象和设备堆栈](https://msdn.microsoft.com/library/windows/hardware/ff565639)。

- 已根据中的建议编写一个卸载例程[编写卸载例程](https://msdn.microsoft.com/library/windows/hardware/ff566400)。

- 声明使用中所述的函数角色类型声明的每个调度函数[使用函数角色类型声明](using-function-role-type-declarations.md)。 有关 WDM 角色类型信息和 **\_调度\_类型\_(** <em>类型</em> **)** 批注，请参阅[函数用于 WDM 驱动程序函数的角色类型声明](declaring-functions-using-function-role-types-for-wdm-drivers.md)。

若要验证 KMDF 驱动程序的 SDV，为驱动程序必须：

-   包括 Wdf.h 和 Ntddk.h。

-   创建 KMDF 对象中所述[使用框架来开发驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff545545)。

-   批注使用 SDV KMDF 回调函数角色类型中, 所述的每个回调函数[使用函数角色类型声明](using-function-role-type-declarations.md)。 有关受支持的角色类型的列表，请参阅[静态验证工具 KMDF 驱动程序函数声明](static-driver-verifier-kmdf-function-declarations.md)。

若要验证的 NDIS 驱动程序的 SDV，对于该驱动程序必须：

-   包括 Ndis.h 和 Ntddk.h。

-   遵循中的准则[网络设计指南](https://msdn.microsoft.com/library/windows/hardware/ff568356)若要创建的 NDIS 驱动程序。

-   通过使用 SDV NDIS 回调函数角色类型，批注的每个回调函数中所述[使用函数角色类型声明](using-function-role-type-declarations.md)。 有关受支持的角色类型的列表，请参阅[静态验证工具 NDIS 驱动程序函数声明](static-driver-verifier-ndis-function-declarations.md)。

此外，SDV 可以验证支持的驱动程序：

-   [Plug and Play](https://msdn.microsoft.com/library/windows/hardware/ff547125)。

-   [电源管理](https://msdn.microsoft.com/library/windows/hardware/ff547131)。

-   [Windows Management Instrumentation](https://msdn.microsoft.com/library/windows/hardware/ff547139) (WMI)。

### <a name="span-idreservedfunctionnamesspanspan-idreservedfunctionnamesspanreserved-function-names"></a><span id="reserved_function_names"></span><span id="RESERVED_FUNCTION_NAMES"></span>保留的函数名称

SDV[验证引擎](verification-engine.md)驱动程序或库代码时使用 SDV 在内部使用的相同函数名称模式无法正常运行。

具体而言，SDV 不会正确解释代码如果：

-   此代码包含函数名称开头\_ \_init 并后接一个或多个整数，例如\_ \_init123。

-   此代码包含函数名称开头 sdv\_，如 sdv\_Func，或包含字符串\_sdv\_，如 Func\_sdv\_或 Func\_sdv\_foo。

-   库使用.def 文件重命名一个导出的函数和外部名称是库中的另一个静态函数的名称相同。

如果驱动程序代码或库代码包括以下这些元素，SDV 尝试验证该驱动程序或处理库，但会得到**不支持功能 (NSF)** 。 SDV 结果有关的详细信息，请参阅[解释静态驱动程序验证工具结果](interpreting-static-driver-verifier-results.md)。

 

 






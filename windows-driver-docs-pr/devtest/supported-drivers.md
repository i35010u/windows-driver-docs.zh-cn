---
title: 支持的驱动程序
description: 支持的驱动程序
ms.assetid: 1d41a9a9-415a-4dba-8b52-138c47ad63fd
keywords:
- 静态驱动程序验证程序 WDK，要求
- StaticDV WDK，要求
- SDV WDK，要求
- 函数原型 WDK 静态驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d1e4addfd60431623ef7217003180818c98e656
ms.sourcegitcommit: e2de6b9ffb5c7356deb864f9da879533f49b25bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/03/2020
ms.locfileid: "91702612"
---
# <a name="supported-drivers"></a>支持的驱动程序

为了使 SDV 能够验证驱动程序，该驱动程序必须能够解释驱动程序代码，具体而言，就是驱动程序的入口点以及支持所需驱动程序功能的函数和例程中的代码。

以下各节介绍了驱动程序的基本要求，以及 SDV 希望其验证的驱动程序所需的特定语法。 SDV 不会验证驱动程序是否符合这些要求，但如果该驱动程序不符合，则 SDV 可能无法运行，在极少数情况下，它会报告误报或误报结果，因为有误解。

## <a name="basic-driver-characteristics"></a>基本驱动程序特征

SDV 只能验证具有以下特征的驱动程序：

- SDV 验证用 C 和 c + + 编写的驱动程序和库。

- SDV 仅对 KMDF 兼容的设备驱动程序和与 WDM 兼容的设备驱动程序执行完全验证， (功能驱动程序、筛选器驱动程序和总线驱动程序) 、NDIS 驱动程序 (筛选器、微型端口和协议驱动程序) 以及 Storport 驱动程序。

- SDV 尝试对不属于以上类别的驱动程序的泛型属性 (（例如 [NullCheck](nullcheckw.md)) ）进行有限的验证。

- SDV 可以通过使用 WDM 函数角色类型来验证用于声明其驱动程序回调函数的 WDM 驱动程序。 有关如何声明函数的信息，请参阅 [使用 WDM 驱动程序的函数角色类型声明函数](declaring-functions-using-function-role-types-for-wdm-drivers.md)。

- SDV 可以验证从 [内核模式驱动程序框架](../wdf/index.md)生成的驱动程序，前提是使用 SDV-KMDF 回调函数角色类型声明每个回调函数。 有关详细信息，请参阅 [使用 KMDF 驱动程序的函数角色类型声明函数](static-driver-verifier-kmdf-function-declarations.md)。

- SDV 可以验证 NDIS 驱动程序，前提是使用 SDV 回调函数类型通过函数声明为每个回调函数添加注释。 有关详细信息，请参阅 [使用 NDIS 驱动程序的函数角色类型声明函数](static-driver-verifier-ndis-function-declarations.md)。

- SDV 可以验证 Storport 驱动程序，前提是你为每个回调函数添加了函数声明。 可以使用 SDV-Storport 回调函数类型执行此操作。 有关详细信息，请参阅 [使用 Storport 驱动程序的函数角色类型声明函数](declaring-functions-by-using-function-role-types-for-storport-drivers.md)。

### <a name="basic-driver-requirements"></a>基本驱动程序要求

对于 SDV 验证 WDM 驱动程序，该驱动程序必须：

- 包括 Wdm .h 或 Ntddk (Ntddk 是) 的子集。

- 使用 [设备对象简介](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-device-objects) 和后面所述的方法创建设备对象。

- 有一个在 [编写卸载例程](../kernel/writing-an-unload-routine.md)时按建议编写的 unload 例程。

- 使用函数角色类型声明声明每个调度函数，如 [使用函数角色类型声明](using-function-role-type-declarations.md)中所述。 有关 WDM 角色类型和** \_ 调度 \_ 类型 \_ (*类型*) **注释的信息，请参阅[使用 WDM 驱动程序的函数角色类型声明函数](declaring-functions-using-function-role-types-for-wdm-drivers.md)。

对于 SDV 验证 KMDF 驱动程序的驱动程序，该驱动程序必须：

- 包含 Wdf 和 Ntddk。

- 创建 [使用框架开发驱动程序](../wdf/using-the-framework-to-develop-a-driver.md)中所述的 KMDF 对象。

- 使用 SDV-KMDF 回调函数角色注释每个回调函数，如 [使用函数角色类型声明](using-function-role-type-declarations.md)中所述。 有关支持的角色类型的列表，请参阅 [Static Driver VERIFIER KMDF Function 声明](static-driver-verifier-kmdf-function-declarations.md)。

对于 SDV 验证 NDIS 驱动程序，该驱动程序必须：

- 包括 Ndis .h 和 Ntddk。

- 按照 [网络设计指南](../network/index.md) 中的准则创建 NDIS 驱动程序。

- 使用 SDV 回调函数角色类型对每个回调函数添加批注，如 [使用函数角色类型声明](using-function-role-type-declarations.md)中所述。 有关支持的角色类型的列表，请参阅 [静态驱动程序验证器 NDIS 函数声明](static-driver-verifier-ndis-function-declarations.md)。

此外，SDV 可以验证支持的驱动程序：

- [即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)。

- [电源管理](../kernel/introduction-to-power-management.md)。

-  (WMI) [Windows Management Instrumentation](../kernel/implementing-wmi.md) 。

### <a name="reserved-function-names"></a>保留的函数名称

当驱动程序或库代码使用 SDV 在内部使用的相同函数名称模式时，SDV [验证引擎](verification-engine.md) 不能正常运行。

具体而言，在以下情况下，SDV 不会正确解释代码：

- 此代码包括以 \_ \_ init 开头并且后跟一个或多个整数（如 init123）的函数名称 \_ \_ 。

- 此代码包括以 sdv 开头的函数名称（ \_ 如 sdv \_ Func），或包含字符串 \_ Sdv \_ ，如 func \_ sdv \_ 或 func \_ sdv \_ foo。

- 库使用 .def 文件来重命名已导出的函数，外部名称与库中其他静态函数的名称相同。

如果驱动程序代码或库代码包含这些元素，则 SDV 会尝试验证驱动程序或处理库，但 **不支持 (NSF) **的结果。 有关 SDV 结果的详细信息，请参阅 [解释静态驱动程序验证程序结果](interpreting-static-driver-verifier-results.md)。

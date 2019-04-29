---
title: 初始化筛选器驱动程序
description: 初始化筛选器驱动程序
ms.assetid: e24b18b5-76d3-4d56-bf60-0dea91ba014e
keywords:
- 筛选器驱动程序 WDK 连接网络、 初始化
- NDIS 筛选器驱动程序 WDK，初始化
- 初始化筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c724458910c7582cff610c1582f1905d53c5664
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379821"
---
# <a name="initializing-a-filter-driver"></a>初始化筛选器驱动程序



筛选器驱动程序初始化后立即发生在系统加载驱动程序。 筛选器驱动程序作为系统服务的负载。 系统可以在任何时间之前、 期间或微型端口驱动程序加载后加载筛选器驱动程序。 筛选器驱动程序支持的类型的微型端口适配器变得可用，并且筛选器驱动程序初始化完成后，NDIS 可以将筛选器模块附加到的微型端口适配器。

启动驱动程序堆栈时，系统将加载筛选器驱动程序，如果它们不是已加载。 有关启动一个驱动程序堆栈，包括筛选器模块的详细信息，请参阅[启动驱动程序堆栈](starting-a-driver-stack.md)。

筛选器驱动程序加载后，系统会调用驱动程序的[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程。 

系统将为两个参数传递[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113):

-   指向已通过 I/O 系统的驱动程序对象的指针。

-   指定存储特定于驱动程序的参数的位置的注册表路径指向的指针。

[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)返回 STATUS_SUCCESS 或其等效的 NDIS_STATUS_SUCCESS，如果该驱动程序已成功注册为 NDIS 筛选器驱动程序。 如果**DriverEntry**传播返回的错误状态将失败并初始化**NdisXxx**函数或通过内核模式下支持例程，该驱动程序将不继续加载。 **DriverEntry**必须执行同步; 即，它不能返回 STATUS_PENDING 或其等效 NDIS_STATUS_PENDING。

筛选器驱动程序驱动程序将对象传递给[NdisFRegisterFilterDriver](https://msdn.microsoft.com/library/windows/hardware/ff562608)时它会向 NDIS 筛选器驱动程序作为注册的功能。 该驱动程序可以使用注册表路径来获取配置信息。 有关如何访问筛选器驱动程序配置信息的详细信息，请参阅[访问筛选器驱动程序的配置信息](accessing-configuration-information-for-a-filter-driver.md)。

筛选器驱动程序调用**NdisFRegisterFilterDriver**从其**DriverEntry**例程。 筛选器驱动程序导出的一组*FilterXxx*函数通过传递[ **NDIS\_筛选器\_驱动程序\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff565515)结构**NdisFRegisterFilterDriver**处*FilterCharacteristics*参数。

NDIS\_筛选器\_驱动程序\_特征结构指定必需的和可选的入口点*FilterXxx*函数。 可以跳过一些可选函数。 绕过函数的详细信息，请参阅[数据绕过模式](data-bypass-mode.md)。

驱动程序调用[NdisFRegisterFilterDriver](https://msdn.microsoft.com/library/windows/hardware/ff562608)必须做好的任何直接调用其*FilterXxx*函数。

NDIS\_筛选器\_驱动程序\_特征结构对于这些必需指定入口点*FilterXxx*函数：

[*FilterAttach*](https://msdn.microsoft.com/library/windows/hardware/ff549905)

[*FilterDetach*](https://msdn.microsoft.com/library/windows/hardware/ff549918)

[*FilterRestart*](https://msdn.microsoft.com/library/windows/hardware/ff549962)

[*FilterPause*](https://msdn.microsoft.com/library/windows/hardware/ff549957)

NDIS\_筛选器\_驱动程序\_特征结构指定的入口点为可选的且不在运行时可更改这些*FilterXxx*函数：

[*FilterSetOptions*](https://msdn.microsoft.com/library/windows/hardware/ff549972)

[*FilterSetModuleOptions*](https://msdn.microsoft.com/library/windows/hardware/ff549970)

[*FilterOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff549954)

[*FilterOidRequestComplete*](https://msdn.microsoft.com/library/windows/hardware/ff549956)

[*FilterStatus*](https://msdn.microsoft.com/library/windows/hardware/ff549973)

[*FilterNetPnPEvent*](https://msdn.microsoft.com/library/windows/hardware/ff549952)

[*FilterDevicePnPEventNotify*](https://msdn.microsoft.com/library/windows/hardware/ff549926)

[*FilterCancelSendNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff549915)

NDIS\_筛选器\_驱动程序\_特征结构指定的默认入口点为可选的并在运行时，可以更改这些*FilterXxx*函数：

[*FilterSendNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff549966)

[*FilterSendNetBufferListsComplete*](https://msdn.microsoft.com/library/windows/hardware/ff549967)

[*FilterReturnNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff549964)

[*FilterReceiveNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff549960)

中也定义了前面的四个函数[ **NDIS\_筛选器\_分部\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff565544)结构。 此结构指定的函数，可通过调用在运行时更改[ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)函数从[ *FilterSetModuleOptions*](https://msdn.microsoft.com/library/windows/hardware/ff549970)函数。 如果筛选器驱动程序将更改这些部分的特征，在运行时，它必须提供的入口点*FilterSetModuleOptions*。 部分特性可为每个筛选器模块不同。 有关详细信息，请参阅[启动筛选器模块](starting-a-filter-module.md)。

NDIS 调用*FilterSetOptions*函数的调用上下文中**NdisFRegisterFilterDriver**。 *FilterSetOptions*注册 NDIS 可选服务。 有关详细信息，请参阅[配置可选的筛选器驱动程序服务](configuring-optional-filter-driver-services.md)。

如果在调用**NdisFRegisterFilterDriver**成功，NDIS 填充该变量在*NdisFilterDriverHandle*与筛选器驱动程序句柄。 筛选器驱动程序将保存此句柄和更高版本将传递此句柄到 NDIS 函数，如[ **NdisFDeregisterFilterDriver**](https://msdn.microsoft.com/library/windows/hardware/ff561800)，需要作为输入参数的筛选器驱动程序句柄。 当卸载该驱动程序时，它必须调用**NdisFDeregisterFilterDriver**函数，以释放分配的驱动程序资源**NdisFRegisterFilterDriver**。

之后*FilterSetOptions*返回时，筛选器模块位于*Detached*状态。 NDIS 可以调用筛选器驱动程序[ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)函数在调用任何时候*FilterSetOptions*返回。 该驱动程序执行中的筛选器特定于模块的初始化*FilterAttach*函数。 有关将筛选器模块附加到驱动程序堆栈的详细信息，请参阅[附加筛选器模块](attaching-a-filter-module.md)。

筛选器驱动程序还执行要求中的任何其他特定于驱动程序初始化**DriverEntry**。 筛选器驱动程序必须释放它分配中的特定于驱动程序的资源及其[ *FilterDriverUnload* ](https://msdn.microsoft.com/library/windows/hardware/ff549936)例程。 有关详细信息，请参阅[卸载筛选器驱动程序](unloading-a-filter-driver.md)。

 

 






---
title: 网络模块分离
description: 网络模块分离
ms.assetid: f41ac030-0bfc-47e2-9840-2c3550bc7d33
keywords:
- 网络模块 WDK 网络模块注册机构，分离
- 提供程序模块 WDK 网络模块注册机构，分离
- 分离网络模块
- 客户端模块 WDK 网络模块注册机构，分离
- 取消注册网络模块
- 网络模块注册机构 WDK，分离网络模块
- NMR WDK，分离网络模块
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8a677d9076f871cbeb69760f0d0bf8aba4793e9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331889"
---
# <a name="network-module-detachment"></a>网络模块分离


当客户端模块或提供程序模块注销与网络模块注册机构 (NMR) 时，网络模块的附加的对均与相互分离。 客户端模块会向 NMR 通过调用[ **NmrDeregisterClient** ](https://msdn.microsoft.com/library/windows/hardware/ff568774)函数和提供程序模块通过调用注销与 NMR [ **NmrDeregisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568778)函数。 下图演示了模块启动注销的网络。

![取消注册的说明启动的网络模块的关系图](images/nmrdetach1.png)

当任一网络模块会向 NMR 时，NMR 会调用这两个客户端模块的[ *ClientDetachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544908)回调函数，并提供程序模块[ *ProviderDetachClient* ](https://msdn.microsoft.com/library/windows/hardware/ff570397)启动分离网络模块的回调函数。 下图说明了启动中分离 NMR。

![说明启动中分离 nmr 的关系图](images/nmrdetach2.png)

如果客户端模块不能立即从提供程序模块分离本身，则会调用[ **NmrClientDetachProviderComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff568772)函数后分离本身从提供程序模块。 同样，如果提供程序模块不能分离客户端模块立即，则会调用[ **NmrProviderDetachClientComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff568781)后完成分离本身从正常客户端模块。 下图说明了完成中分离的网络模块。

![说明完成分离的网络模块的关系图](images/nmrdetach3.png)


NMR 客户端模块和提供程序模块已完成从彼此分离后，调用客户端模块[ *ClientCleanupBindingContext* ](https://msdn.microsoft.com/library/windows/hardware/ff544904)回调函数和提供程序模块的[ *ProviderCleanupBindingContext* ](https://msdn.microsoft.com/library/windows/hardware/ff570396)回调函数，以便网络模块可以清理附件其各自的绑定上下文。 下图说明了 NMR 起始清理。

![说明 nmr 起始清理的关系图](images/nmrdetach4.png)


如果已经取消了客户端模块，并注册 NMR，客户端模块注销直到才会完成客户端模块已从所有提供程序模块，它以前被附加到所有这些提供程序模块具有完全分离从客户端模块完全分离。 客户端模块等待通过调用来完成注销[ **NmrWaitForClientDeregisterComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff568786)函数。 同样，如果与 NMR 取消注册提供程序模块，提供程序模块注销直到才会完成的提供程序模块已完全分离所有以前被附加到的客户端模块和所有这些客户端模块从具有完全分离的提供程序模块中。 提供程序模块等待通过调用来完成注销[ **NmrWaitForProviderDeregisterComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff568787)函数。 下图演示了网络模块正在等待注销才能完成。

![说明等待网络模块的关系图完成注销](images/nmrdetach5.png)

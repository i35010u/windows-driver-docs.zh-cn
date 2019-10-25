---
title: 网络编程接口
description: 网络编程接口
ms.assetid: 74d706e1-5398-4685-b3ab-7b4c4b6b5588
keywords:
- NPI WDK 网络模块注册器
- 客户端特征结构 WDK 网络模块注册机构
- 提供程序特征结构 WDK 网络模块注册机构
- 客户端调度表 WDK 网络模块注册器
- 调度表 WDK 网络模块注册器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a507a230834cea92a4ab78022386cc5dbfe65a1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827131"
---
# <a name="network-programming-interface"></a>网络编程接口


*网络编程接口*（或 NPI）定义可彼此连接的[网络模块](network-module.md)之间的接口。 注册为特定 NPI 的客户端的[客户端模块](client-module.md)只能附加到注册为同一 NPI 的提供程序的[提供程序模块](provider-module.md)。 同样，注册为特定 NPI 的提供程序的提供程序模块只能附加到注册为同一 NPI 的客户端的客户端模块。

每个 NPI 定义以下各项：

-   唯一标识 NPI 的*NPI 标识符*。 网络模块指定 NPI 标识符，指示在网络模块将其自身注册到网络模块注册器（NMR）时所支持的特定 NPI。 网络模块可以支持多个 NPIs，方法是将自身注册到 NMR 多次，一次为它支持的每个 NPI 注册一次。 仅当客户端模块支持相同的 NPI 时，NMR 才会开始将客户端模块附加到提供程序模块。

-   可选的[*客户端特征*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_client_characteristics)结构，指定每个客户端模块的 NPI 特定的特征。 此类 NPI 特定的特征可能包括客户端模块支持的 NPI 版本（或客户端模块所需的地址族或协议）等项。 提供程序模块可以使用客户端模块的客户端特征结构中包含的信息来确定它是否会附加到客户端模块。 如果 NPI 未定义任何特定于 NPI 的客户端特征，则不需要此结构。

-   一个可选的[*提供程序特征*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_provider_characteristics)结构，指定每个提供程序模块的 NPI 特定的特征。 此类 NPI 特定的特征可能包括提供程序模块支持的 NPI 版本（或版本），或者提供程序模块支持的地址系列或协议。 客户端模块可以使用提供程序模块的客户端特征结构中包含的信息来确定它是否会附加到提供程序模块。 如果 NPI 未定义任何特定于 NPI 的提供程序特征，则不需要此结构。

-   零个或多个客户端模块回调函数。 在提供程序模块成功附加到客户端模块后，提供程序模块可以通过调用客户端模块的回调函数来访问客户端模块的功能。

-   一个或多个提供程序模块函数。 将客户端模块成功附加到提供程序模块后，客户端模块可以通过调用提供程序模块的函数来访问该提供程序模块的功能。

-   一种*客户端调度表*结构，其中包含指向每个客户端模块回调函数的函数指针。 如果 NPI 未定义任何客户端模块回调函数，则不需要此结构。

-   一种*提供程序调度表*结构，其中包含指向每个提供程序模块函数的函数指针。

支持特定 NPI 的客户端模块使用由 NPI 定义的项来实现接口的客户端。 同样，支持特定 NPI 的提供程序模块使用由 NPI 定义的项来实现接口的提供程序端。

除 NPI 标识符外，NPI 定义的所有项对于 NMR 是不透明的。 NMR 使用 NPI 标识符来确定哪些客户端模块应连接到哪些提供程序模块。

 

 






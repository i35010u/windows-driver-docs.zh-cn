---
title: 网络模块附加
description: 网络模块附加
ms.assetid: 4b3602dd-a9cf-4cb6-bfeb-d2d74d2f391d
keywords:
- 网络模块 WDK 网络模块注册机构，附件
- 提供商模块 WDK 网络模块注册机构，附件
- 客户端模块 WDK 网络模块注册机构，附件
- 附加网络模块
- 正在注册网络模块
- 网络模块注册 WDK，附加网络模块
- NMR WDK，附加网络模块
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1d86f2fe4581a80741f48ef1c2b4782d5d3d54d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827209"
---
# <a name="network-module-attachment"></a>网络模块附加


在将[客户端模块](client-module.md)和[提供程序模块](provider-module.md)附加到另一个提供程序模块之前，每个模块都必须向 NMR 注册自身。 客户端模块通过调用[**NmrRegisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterclient)函数向 NMR 注册，并通过调用[**NMRREGISTERPROVIDER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterprovider)函数向 NMR 注册提供程序模块。 下图说明了网络模块注册。

![阐释网络模块注册的示意图](images/nmrattach1.png)

如果客户端模块和提供程序模块在向 NMR 注册时指定相同的[网络编程接口（NPI）](network-programming-interface.md) ，则 NMR 将同时启动两个网络模块。 NMR 通过调用客户端模块的[*ClientAttachProvider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn)回调函数来启动附件处理。 下图说明了启动附件的网络模块注册器（NMR）。

![说明如何启动附件的网络模块注册器（nmr）的关系图](images/nmrattach2.png)

客户端模块的[*ClientAttachProvider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn)回调函数可以检查提供程序模块的注册数据，以确定它是否会附加到提供程序模块。 如果客户端模块确定它将附加到提供程序模块，则会通过调用[**NmrClientAttachProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientattachprovider)函数继续执行附件过程。 当客户端模块调用**NmrClientAttachProvider**函数时，NMR 反过来调用提供程序模块的[*ProviderAttachClient*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_attach_client_fn)回调函数。 下图说明了继续附件的客户端模块。

![说明客户端模块继续附加的关系图](images/nmrattach3.png)

提供程序模块的[*ProviderAttachClient*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_attach_client_fn)回调函数可以检查客户端模块的注册数据，以确定它是否会附加到客户端模块。 如果提供程序模块确定它将附加到客户端模块，则提供程序模块和客户端模块会交换指向其各自的 NPI 调度表结构的指针。 附加客户端模块和提供程序模块后，它们可以通过独立于 NMR 的 NPI 函数互相交互。 下图说明了附加的网络模块。

![阐释连接的网络模块的关系图](images/nmrattach4.png)

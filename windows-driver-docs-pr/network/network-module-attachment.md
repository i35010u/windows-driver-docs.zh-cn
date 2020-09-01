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
ms.openlocfilehash: 6905e7d9f81957c9be50e5e1d29cc4f601fd3997
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210675"
---
# <a name="network-module-attachment"></a>网络模块附加


在将 [客户端模块](client-module.md) 和 [提供程序模块](provider-module.md) 附加到另一个提供程序模块之前，每个模块都必须向 NMR 注册自身。 客户端模块通过调用 [**NmrRegisterClient**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterclient) 函数向 NMR 注册，并通过调用 [**NMRREGISTERPROVIDER**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterprovider) 函数向 NMR 注册提供程序模块。 下图说明了网络模块注册。

![阐释网络模块注册的示意图](images/nmrattach1.png)

如果客户端模块和提供程序模块在向 NMR 注册 [ () NPI ](network-programming-interface.md) 时指定相同的网络编程接口，则 NMR 将启动将两个网络模块一起附加。 NMR 通过调用客户端模块的 [*ClientAttachProvider*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn) 回调函数来启动附件处理。 下图说明了 (NMR) 启动附件的网络模块注册器。

![说明网络模块注册器 (nmr) 启动附件的示意图](images/nmrattach2.png)

客户端模块的 [*ClientAttachProvider*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn) 回调函数可以检查提供程序模块的注册数据，以确定它是否会附加到提供程序模块。 如果客户端模块确定它将附加到提供程序模块，则会通过调用 [**NmrClientAttachProvider**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientattachprovider) 函数继续执行附件过程。 当客户端模块调用 **NmrClientAttachProvider** 函数时，NMR 反过来调用提供程序模块的 [*ProviderAttachClient*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_attach_client_fn) 回调函数。 下图说明了继续附件的客户端模块。

![说明客户端模块继续附加的关系图](images/nmrattach3.png)

提供程序模块的 [*ProviderAttachClient*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_attach_client_fn) 回调函数可以检查客户端模块的注册数据，以确定它是否会附加到客户端模块。 如果提供程序模块确定它将附加到客户端模块，则提供程序模块和客户端模块会交换指向其各自的 NPI 调度表结构的指针。 附加客户端模块和提供程序模块后，它们可以通过独立于 NMR 的 NPI 函数互相交互。 下图说明了附加的网络模块。

![阐释连接的网络模块的关系图](images/nmrattach4.png)
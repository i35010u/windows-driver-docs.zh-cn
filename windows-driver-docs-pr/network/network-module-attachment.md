---
title: 网络模块附加
description: 网络模块附加
ms.assetid: 4b3602dd-a9cf-4cb6-bfeb-d2d74d2f391d
keywords:
- 网络模块 WDK 网络模块注册机构，附件
- 提供程序模块 WDK 网络模块注册机构，附件
- 客户端模块 WDK 网络模块注册机构，附件
- 附加网络模块
- 注册网络模块
- 网络模块注册机构 WDK，附加网络模块
- NMR WDK，附加网络模块
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a65ef5bba34bc3712b6e3c42834831778a1e049
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386330"
---
# <a name="network-module-attachment"></a>网络模块附加


之前[客户端模块](client-module.md)和一个[提供程序模块](provider-module.md)可以附加到彼此，它们都必须向进行自行注册 NMR。 客户端模块向 NMR 注册通过调用[ **NmrRegisterClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrregisterclient)函数和提供程序注册通过调用 NMR 模块[ **NmrRegisterProvider** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrregisterprovider)函数。 下图演示了网络模块注册。

![说明网络模块注册的关系图](images/nmrattach1.png)

如果客户端模块和提供程序模块都指定相同[网络编程接口 (NPI)](network-programming-interface.md) NMR 时向 NMR 注册它们，请将启动一起附加两个网络模块。 NMR 启动附加过程通过调用客户端模块[ *ClientAttachProvider* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_client_attach_provider_fn)回调函数。 下图演示了网络模块注册机构 (NMR) 启动该附件。

![说明网络模块注册机构 (nmr) 的启动附件的关系图](images/nmrattach2.png)

客户端模块[ *ClientAttachProvider* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_client_attach_provider_fn)回调函数可以检查提供程序模块，以确定它将附加到提供程序模块的注册数据。 如果客户端模块确定它会将连接到提供程序模块，它会在附加过程继续通过调用[ **NmrClientAttachProvider** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrclientattachprovider)函数。 当客户端模块调用**NmrClientAttachProvider**函数，NMR 反过来调用提供程序模块[ *ProviderAttachClient* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_provider_attach_client_fn)回调函数。 下图说明了客户端模块继续附件。

![说明客户端模块继续附件的关系图](images/nmrattach3.png)

提供程序模块[ *ProviderAttachClient* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_provider_attach_client_fn)回调函数可以检查客户端模块，以确定它将附加到客户端模块的注册数据。 如果提供程序模块确定它会将连接到客户端模块，提供程序模块和客户端模块交换其各自的 NPI 调度表结构的指针。 附加到客户端模块和提供程序模型后，它们可以彼此交互通过独立于 NMR 其 NPI 函数。 下图说明了附加的网络模块。

![说明附加的网络模块的关系图](images/nmrattach4.png)

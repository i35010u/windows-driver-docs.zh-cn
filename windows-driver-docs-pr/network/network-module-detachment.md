---
title: 网络模块分离
description: 网络模块分离
ms.assetid: f41ac030-0bfc-47e2-9840-2c3550bc7d33
keywords:
- 网络模块 WDK 网络模块注册器，分离
- 提供程序模块 WDK 网络模块注册器，分离
- 分离网络模块
- 客户端模块 WDK 网络模块注册器，分离
- 注销网络模块
- 网络模块注册 WDK，分离网络模块
- NMR WDK，分离网络模块
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8acf93c3b32757f40ba1ca062a56382bc1bb4566
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827159"
---
# <a name="network-module-detachment"></a>网络模块分离


当客户端模块或提供程序模块与网络模块注册机构（NMR）注销时，附加的网络模块将相互分离。 通过调用[**NMR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterprovider)函数，使用 NmrDeregisterProvider 调用[**NmrDeregisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterclient)函数和提供程序模块注销，注销与 NMR 的客户端模块。 下图说明了启动注销的网络模块。

![说明启动取消注册的网络模块的示意图](images/nmrdetach1.png)

当任一网络模块与 NMR 注销时，NMR 都将调用客户端模块的[*ClientDetachProvider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_detach_provider_fn)回调函数和提供程序模块的[*ProviderDetachClient*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_detach_client_fn)回调函数以启动分离网络模块。 下图说明了启动分离的 NMR。

![说明启动分离的 nmr 的示意图](images/nmrdetach2.png)

如果客户端模块无法立即从提供程序模块分离自身，则它会在完成从提供程序模块分离自身后调用[**NmrClientDetachProviderComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientdetachprovidercomplete)函数。 同样，如果提供程序模块无法立即从客户端模块分离自身，则它会在完成从客户端模块分离自身后调用[**NmrProviderDetachClientComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrproviderdetachclientcomplete)函数。 下图说明了完成分离的网络模块。

![说明完成分离的网络模块的关系图](images/nmrdetach3.png)


在客户端模块和提供程序模块彼此分离完成后，NMR 将调用客户端模块的[*ClientCleanupBindingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_cleanup_binding_context_fn)回调函数和提供程序模块的[*ProviderCleanupBindingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_cleanup_binding_context_fn)回调函数，以便网络模块可以清理其各自的连接绑定上下文。 下图说明了 NMR 开始清除。

![说明 nmr 启动清理的示意图](images/nmrdetach4.png)


如果客户端模块取消注册到 NMR，则在客户端模块与以前附加到的所有提供程序模块完全分离并且所有这些提供程序模块都具有与客户端模块完全分离。 客户端模块通过调用[**NmrWaitForClientDeregisterComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrwaitforclientderegistercomplete)函数等待注销完成。 同样，如果提供程序模块取消注册到 NMR，则在提供程序模块与以前附加到的所有客户端模块和所有这些客户端模块完全分离之前，不会完成提供程序模块的取消注册。与提供程序模块完全分离。 提供程序模块通过调用[**NmrWaitForProviderDeregisterComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrwaitforproviderderegistercomplete)函数等待注销完成。 下图说明了等待注销完成的网络模块。

![说明等待注销完成的网络模块的关系图](images/nmrdetach5.png)

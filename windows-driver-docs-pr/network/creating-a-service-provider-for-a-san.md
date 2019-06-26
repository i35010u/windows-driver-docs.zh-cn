---
title: 创建 SAN 的服务提供程序
description: 创建 SAN 的服务提供程序
ms.assetid: 848b6fd5-64f8-4e62-9c54-c23bbc3d9ede
keywords:
- Windows 套接字直接 WDK，服务提供商
- SAN 服务提供商 WDK，创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05a53136415eb5ce43effe5124789ecfae26e59c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374927"
---
# <a name="creating-a-service-provider-for-a-san"></a>创建 SAN 的服务提供程序





本部分提供对 SAN 服务提供程序 DLL 和 Windows 套接字交换机之间的接口组成函数的简要说明。 SAN 服务提供程序 DLL 导出其初始化函数的单入口点[ **WSPStartupEx**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566321(v=vs.85))。 SAN 服务提供商**WSPStartupEx**函数又使大多数其他接口函数可访问到调度表通过 Windows 套接字交换机。 其余的接口函数提供给通过调用 SAN 服务提供商的交换机[ **WSPIoctl** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566296(v=vs.85))函数。 接口函数包括[Windows 套接字 SPI 函数](windows-sockets-spi-functions-required-for-sans.md)并[SAN 特定于 Windows 套接字 SPI 接口扩展](windows-sockets-spi-extensions-for-sans.md)。

[Windows 套接字直接引用](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565857(v=vs.85))提供了有关这些函数的详细的信息，如 SAN 服务提供程序中实现。 不要使用 Windows 套接字 SPI 函数的 Microsoft Windows SDK 说明。 Windows SDK 说明不包含特定于 SAN 的要求。

本部分还列出了[SAN 服务提供程序不是 Windows 套接字 SPI 函数要求提供](windows-sockets-spi-functions-not-required-for-sans.md)。

 

 






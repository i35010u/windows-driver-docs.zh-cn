---
title: 网络模块注册机构的体系结构概述
description: 介绍网络模块注册器的基本体系结构概述
keywords:
- 网络模块注册 WDK，体系结构
- NMR WDK，体系结构
- 体系结构 WDK 网络模块注册商
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09a08a5121db23a173ee9f0624f22df60809649c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813039"
---
# <a name="architecture-overview-for-the-network-module-registrar"></a>网络模块注册机构的体系结构概述

下图显示了 (NMR) 的网络模块注册器的基本体系结构概述：

![阐释网络模块注册器 (nmr 的基本体系结构的关系图) ](images/nmrarch.png)

在这种情况下，有两个 [网络模块](network-module.md)： [客户端模块](client-module.md) 和 [提供程序模块](provider-module.md)。 客户端模块和提供程序模块分别是客户端和同一 [网络编程接口的提供程序 (NPI) ](network-programming-interface.md)。 每个网络模块都直接与 NMR 交互，目的是注册和注销，并附加到其他网络模块以及从中分离。 仅当客户端模块支持相同的 NPI 时，NMR 才会开始将客户端模块附加到提供程序模块。 将客户端模块和提供程序模块彼此连接后，它们可以通过独立于 NMR 的 NPI 函数互相交互。

以下各节概述了支持公共 NPI 的客户端模块和提供程序模块的附加和分离过程。

[网络模块附加](network-module-attachment.md)

[网络模块分离](network-module-detachment.md)

 

 






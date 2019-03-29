---
title: 网络模块注册机构的体系结构概述
description: 介绍适用于的网络模块注册机构的基本体系结构概述
ms.assetid: 7e2c51ed-ecec-4b17-8a6f-42a51acedc95
keywords:
- 网络模块注册机构 WDK，体系结构
- NMR WDK，体系结构
- WDK 网络模块注册机构的体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c51a73444c120d20889f728877da5bdbd6467b1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566243"
---
# <a name="architecture-overview-for-the-network-module-registrar"></a>网络模块注册机构的体系结构概述

下图中所示的基本体系结构的网络模块注册机构 (NMR) 的概述：

![说明网络模块注册机构 (nmr) 的基本体系结构的关系图](images/nmrarch.png)

在这种情况下，有两个[网络模块](network-module.md)即[客户端模块](client-module.md)和一个[提供程序模块](provider-module.md)。 客户端模块，并提供程序模块分别为客户端和提供程序的相同[网络编程接口 (NPI)](network-programming-interface.md)。 每个网络模块直接与实现注册而 NMR 交互和注销，以及将附加到，和从其他网络模块中分离。 NMR 将启动客户端模块附加到提供程序模块，仅当它们都支持相同 NPI。 相互连接的客户端模块和提供程序模块后，它们可以彼此交互通过独立于 NMR 其 NPI 函数。

以下各节提供过程的概述，由客户端模块和提供程序模块都支持常见 NPI 附加和分离。

[网络模块附件](network-module-attachment.md)

[网络模块分离](network-module-detachment.md)

 

 






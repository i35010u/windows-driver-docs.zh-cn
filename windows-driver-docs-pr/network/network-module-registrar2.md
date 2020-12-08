---
title: 网络模块注册机构主题
description: 网络模块注册机构主题
keywords:
- 网络模块注册 WDK
- NMR WDK
- 模块 WDK 网络模块注册器
- 已注册的网络模块 WDK 网络模块注册器
- 软件模块 WDK 网络模块注册器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01869d1074b1d143ae391ecb797e704471bfc4e3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840303"
---
# <a name="network-module-registrar-topics"></a>网络模块注册机构主题


本部分讨论网络模块注册器，并包括以下主题：

[网络模块注册机构简介](introduction-to-the-network-module-registrar.md)

[网络模块](network-module.md)

[体系结构概述](architecture-overview.md)

[初始化和注册客户端模块](initializing-and-registering-a-client-module.md)

[提供程序模块操作](initializing-and-registering-a-provider-module.md)

[编程注意事项](programming-considerations.md)

使用 [**WskRegister**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskregister) 和 [**WskDeregister**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskderegister) 函数是注册和注销 WSK 应用程序的首选方法。 网络模块注册机构仍可提供兼容性。 有关详细信息，请参阅 [注册 Winsock 内核应用程序](registering-a-winsock-kernel-application.md)。

 


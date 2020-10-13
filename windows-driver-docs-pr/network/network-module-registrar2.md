---
title: 网络模块注册机构主题
description: 网络模块注册机构主题
ms.assetid: 23c15c42-94aa-410b-8551-fafa8b24ad86
keywords:
- 网络模块注册 WDK
- NMR WDK
- 模块 WDK 网络模块注册器
- 已注册的网络模块 WDK 网络模块注册器
- 软件模块 WDK 网络模块注册器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5d14529a4039d3e9e98fdd7b81f08dbc119f1fc
ms.sourcegitcommit: db9d058a9e592d4c47c67fc14f04f0ddc3aa92af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "91989845"
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

 


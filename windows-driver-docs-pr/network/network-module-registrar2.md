---
title: 网络模块注册机构
description: 网络模块注册机构
ms.assetid: 23c15c42-94aa-410b-8551-fafa8b24ad86
keywords:
- 网络模块注册机构 WDK
- NMR WDK
- 模块 WDK 网络模块注册机构
- 已注册的网络模块 WDK 网络模块注册机构
- 软件模块 WDK 网络模块注册机构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa2fe60c1528355adff70664ca9744933d75b580
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386321"
---
# <a name="network-module-registrar"></a>网络模块注册机构


本部分讨论了网络模块注册机构，包括以下主题：

[网络模块注册机构的简介](introduction-to-the-network-module-registrar.md)

[网络模块注册机构定义](nmr-definitions.md)

[体系结构概述](architecture-overview.md)

[客户端模块操作](client-module-operations.md)

[提供程序模块操作](provider-module-operations.md)

[编程注意事项](programming-considerations.md)

使用[ **WskRegister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskregister)并[ **WskDeregister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskderegister)函数是用于注册和注销 WSK 的首选的方法应用程序。 网络模块注册机构可保留用于兼容性。 有关详细信息，请参阅[Winsock 内核应用程序注册](registering-a-winsock-kernel-application.md)。

 

 






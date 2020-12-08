---
title: 使用 NMR 注册和取消注册 WSK
description: 使用 NMR 注册和取消注册 WSK
keywords:
- Winsock 内核 WDK 网络，注册
- 注册 Winsock 内核应用程序
- WSK WDK 网络，注册
- 注销 Winsock 内核应用程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 581162ff83196ab4ae43617212247db463a9d58f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806137"
---
# <a name="using-nmr-for-wsk-registration-and-unregistration"></a>使用 NMR 注册和取消注册 WSK


[注册 Winsock 内核应用程序](registering-a-winsock-kernel-application.md)和取消[注册 Winsock 内核应用程序](unregistering-a-winsock-kernel-application.md)部分说明了 WSK 应用程序如何使用[WSK 注册函数](/windows-hardware/drivers/ddi/_netvista/)附加到 WSK 子系统并从其分离。 但是，WSK 还可以通过使用 [网络模块注册器 (NMR) ](network-module-registrar2.md)附加到 WSK 子系统。

WSK 应用程序可以通过使用以下部分中的过程，将 NMR 作为 WSK 网络编程接口的客户端注册 [ (NPI) ](network-programming-interface.md) ：

-   [初始化 NMR 数据结构](initializing-nmr-data-structures.md)
-   [将 WSK 客户端附加到 WSK 子系统](attaching-the-wsk-client-to-the-wsk-subsystem.md)
-   [取消注册和卸载 WSK 客户端](unregistering-and-unloading-the-wsk-client.md)

使用 [**WskRegister**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskregister) 和 [**WskDeregister**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskderegister) 函数是注册和注销 WSK 应用程序的首选方法。 [网络模块注册机构](network-module-registrar2.md)仍可提供兼容性。

 


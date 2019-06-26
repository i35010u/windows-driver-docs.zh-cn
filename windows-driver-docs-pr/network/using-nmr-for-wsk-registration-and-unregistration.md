---
title: 使用 NMR 注册和取消注册 WSK
description: 使用 NMR 注册和取消注册 WSK
ms.assetid: 942fb4e6-ec2e-47ab-9b40-2bd0b7c72ec0
keywords:
- Winsock 内核 WDK 连接网络、 注册
- 注册 Winsock 内核应用程序
- WSK WDK 连接网络、 注册
- 正在注销 Winsock 内核应用程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e2726300dcfa42b2eb8b5359dd8e54415369c21
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371780"
---
# <a name="using-nmr-for-wsk-registration-and-unregistration"></a>使用 NMR 注册和取消注册 WSK


[Winsock 内核应用程序注册](registering-a-winsock-kernel-application.md)并[Winsock 内核应用程序中注销](unregistering-a-winsock-kernel-application.md)各节介绍如何将附加到和从 WSK 子系统通过使用分离WSK应用程序[WSK 注册函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)。 但是，WSK 还能够附加到 WSK 子系统通过使用[网络模块注册机构 (NMR)](network-module-registrar2.md)。

WSK 应用程序可将自身注册 NMR 作为客户端 WSK[网络编程接口 (NPI)](network-programming-interface.md)以下各节中使用的过程：

-   [初始化 NMR 数据结构](initializing-nmr-data-structures.md)
-   [附加到 WSK 子系统 WSK 客户端](attaching-the-wsk-client-to-the-wsk-subsystem.md)
-   [取消注册和卸载 WSK 客户端](unregistering-and-unloading-the-wsk-client.md)

使用[ **WskRegister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskregister)并[ **WskDeregister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskderegister)函数是用于注册和注销 WSK 的首选的方法应用程序。 [网络模块注册机构](network-module-registrar2.md)可保留用于兼容性。

 

 






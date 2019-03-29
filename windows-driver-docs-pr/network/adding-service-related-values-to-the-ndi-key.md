---
title: 将服务相关的值添加到 Ndi 键
description: 将服务相关的值添加到 Ndi 键
ms.assetid: f967396c-6695-458c-a081-ef382ed7c9dd
keywords:
- 添加注册表部分 WDK 网络、 Ndi 值和密钥
- Nido 键和值 WDK 网络
- Ndi 密钥 WDK 网络与服务相关的值
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7badf1f4c35cbcc4349bf267529a4c4f0d271e8d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577129"
---
# <a name="adding-service-related-values-to-the-ndi-key"></a>将服务相关的值添加到 Ndi 键





如果组件具有关联的服务 （设备驱动程序）*添加注册表部分*所引用的*DDInstall*部分对于该组件必须添加**服务**到 Ndi 密钥的值。 **服务**值是 REG\_SZ 值，该值指定与该组件关联的主服务。 **服务**值必须匹配*ServiceName*参数**AddService**指令，它引用*服务安装部分*主服务。 有关详细信息，请参阅[INF DDInstall.Services 部分](ddinstall-services-section-in-a-network-inf-file.md)。

如果组件具有一个或多个关联的服务，*添加注册表部分*所引用的*DDInstall*部分对于该组件必须添加**CoServices**值设为**Ndi**密钥。 **CoServices**值是一个多\_SZ 值，该值指定将安装该组件，包括指定的主服务的所有服务**服务**值。 **CoServices**值是必需的所有**NetTrans**， **NetClient**，以及**NetService**组件。

**请注意**  **NetClient**组件在 Windows 8.1，Windows Server 2012 R2 中已弃用及更高版本。

 

**请注意**  **Net**组件 （适配器） 不应具有**CoServices**值，因为只有一个服务可以与适配器相关联。

 

除了关闭服务，与服务相关的所有操作上都执行**CoServices**中所列的顺序。 例如，服务启动所列的顺序。 停止服务，但是，在相反的顺序。 仅当该服务在服务上执行与服务相关的组件的操作**CoServices**。

 

 






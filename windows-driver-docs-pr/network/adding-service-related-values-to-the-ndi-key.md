---
title: 将服务相关的值添加到 Ndi 键
description: 将服务相关的值添加到 Ndi 键
keywords:
- 添加-注册表--WDK 网络、Ndi 值和密钥
- Nido 密钥和值 WDK 网络
- 与服务相关的值，用于 Ndi 密钥 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92b7f04293cea45ace2d0e9f04ccc5733aa0b699
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792195"
---
# <a name="adding-service-related-values-to-the-ndi-key"></a>将服务相关的值添加到 Ndi 键





如果组件具有关联的服务 (设备驱动程序) ，则该组件的 *DDInstall* 部分引用的 "*添加注册表" 部分* 必须将 **服务** 值添加到 Ndi 项。 **服务** 值为 REG \_ SZ 值，该值指定与组件关联的主服务。 **服务** 值必须与引用主要服务的 *服务安装部分* 的 **AddService** 指令的 *ServiceName* 参数匹配。 有关详细信息，请参阅 [INF DDInstall 部分](ddinstall-services-section-in-a-network-inf-file.md)。

如果某个组件有一个或多个关联服务，则该组件的 *DDInstall* 部分引用的 "*添加注册表" 部分* 必须将 **CoServices** 值添加到 **Ndi** 项。 **CoServices** 值是多个 \_ SZ 值，它指定组件安装的所有服务，包括 **服务** 值指定的主服务。 **CoServices** 值对所有 **NetTrans**、 **NetClient** 和 **空间** 组件都是必需的。

**请注意**，**NetClient** 组件在 Windows 8.1、Windows Server 2012 R2 和更高版本中已弃用。  

 

**请注意**， (适配器的 **网络** 组件) 不应具有 **CoServices** 值，因为一个适配器只能关联一个服务。  

 

除关闭服务外，所有与服务相关的操作都按照列出的顺序在 **CoServices** 上执行。 例如，服务按其列出的顺序启动。 不过，服务会按相反的顺序停止。 仅当服务在 **CoServices** 中列出时，组件的服务相关操作才能在服务中执行。

 

 






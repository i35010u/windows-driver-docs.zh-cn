---
title: 网络模块注册机构的简介
description: 网络模块注册机构的简介
ms.assetid: affa7979-bc43-4e34-a528-5484982d940d
keywords:
- 网络模块注册机构 WDK，有关网络模块注册机构
- NMR WDK，有关网络模块注册机构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11ba64a692753aaa6981352f4aa3ea2568b0c319
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519910"
---
# <a name="introduction-to-the-network-module-registrar"></a>网络模块注册机构的简介


网络模块注册机构 (NMR) 是一个操作系统模块，便于的附件[网络模块](network-module.md)到对方。 向 NMR，指定描述网络模块的特征，每个网络模块注册自身。 NMR 启动对之间可以相互连接的已注册的网络模块的附件。 这些值将附加后，则网络模块独立于 NMR 都可以彼此交互。 NMR 还便于附加对网络模块的分离时的网络模块之一与 NMR 注销。 直到网络模块是从以前附加的所有网络模块完全分离，才会完成网络模块的注销。

尽管 NMR 的开发时使用的网络模块，但 NMR 体系结构的设计是非常通用，以便它也可以使用由其他技术领域中的软件模块。

 

 






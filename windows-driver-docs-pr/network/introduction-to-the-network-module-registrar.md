---
title: 网络模块注册机构简介
description: 网络模块注册机构简介
keywords:
- 网络模块注册 WDK，关于网络模块注册机构
- NMR WDK，关于网络模块注册器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfca39872ab087287a6dc193235140cda2b81d6d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818369"
---
# <a name="introduction-to-the-network-module-registrar"></a>网络模块注册机构简介


网络模块注册器 (NMR) 是一种操作系统模块，有助于 [网络模块](network-module.md) 彼此之间的连接。 每个网络模块都向 NMR 注册自己，并指定描述网络模块的特征。 NMR 在可彼此连接的已注册网络模块对之间发起连接。 附加它们后，网络模块可以彼此独立于 NMR。 NMR 还有助于在其中一个网络模块与 NMR 注销时，分离附加的网络模块对。 在网络模块完全与以前附加到的所有网络模块分离之前，不会完成网络模块的取消注册。

尽管 NMR 是为供网络模块使用而开发的，但 NMR 体系结构的设计是足够通用的，以便其他技术领域的软件模块也能使用它。

 

 






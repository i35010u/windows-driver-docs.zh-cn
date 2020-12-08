---
title: 存储器虚拟微型端口驱动程序概述
description: 存储器虚拟微型端口驱动程序概述
keywords:
- 存储虚拟微型端口驱动程序 WDK，关于
- 虚拟微型端口驱动程序 WDK
- 微型端口驱动程序 WDK 存储，虚拟
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1443562f786b399725b71495a861d7c9ad60c5c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834993"
---
# <a name="overview-of-storage-virtual-miniport-drivers"></a>存储器虚拟微型端口驱动程序概述


为了扩展 Storport 接口的有用性，对于带有 Service Pack 1 (SP1) 和 Windows Server 2008 的 Windows Vista，Microsoft 已定义虚拟小型端口 (VMiniport) 驱动程序接口。 此接口适用于当前与物理硬件无严格关联的微型端口驱动程序。 这些更改不会消除硬件相关 ( "物理" ) 微型端口驱动程序的限制，只调用 Storport 例程。 与物理微型端口驱动程序不同的是，虚拟小型端口驱动程序可以调用 Windows 驱动模型 (WDM) 例程，如 WDM 文档状态。 除非另有说明，否则将使用 "微型端口" 这一术语来表示 "虚拟小型端口"。

虚拟微型端口驱动程序接口释放依赖于端口驱动程序的端口驱动程序 (Storport) 用于处理内存和同步。 接口使虚拟微型端口驱动程序能够以目前不可用的方式执行 i/o。 这些更改的目标是（但不限于）在将来启用 iSCSI 等存储技术，以及非标准存储接口。

实现 VMiniport 驱动程序时，请务必小心。 尽管扩展具有更大的灵活性，但在检测错误、验证路径和 i/o 计时时需要更多的关注。 此处提供一些示例，但无法正确预测使用内核接口的所有可能的结果。

 

 





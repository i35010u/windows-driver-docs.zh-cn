---
title: 从 ScsiPort 移植到 StorPort
description: 从 ScsiPort 移植到 StorPort
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 549ea2e50ecbe91975a0d78336f527dc330bbc9b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785495"
---
# <a name="porting-from-scsiport-to-storport"></a>从 ScsiPort 移植到 StorPort


下面概述了将示例代码从基于 Scsiport 的微型端口驱动程序移植到基于 Storport 的微型端口驱动程序所必需的移植活动：

-   删除所有 NextRequest 和 NextLuRequest 调用

-   将所有 ScsiPortXxx 调用重命名为 StorPortXxx

-   添加 BuildIo 例程 (移动了大约75% 的代码 StartIo) 

-   将驱动程序转换为全双工操作

-   添加队列管理例程 (错误处理、适配器重启) 

-   添加 LUN 和目标重置支持

-   添加代码以在内部分配队列标记 (硬件限制) 

-   为总线重置和完整适配器重启添加同步例程

-   \_通过 SRB) 添加对 SRB 函数 \_ POWER (适配器关闭的支持

-   添加 StorPortSetDeviceQueueDepth 调用--LUN 队列深度设置为31

 

 





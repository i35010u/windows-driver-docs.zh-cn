---
title: 从 ScsiPort 移植到 StorPort
description: 从 ScsiPort 移植到 StorPort
ms.assetid: 2a14051d-dc23-4420-a3e5-0827b16b1e42
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b4868d662d747d964e662280dff9be86aaea6e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533484"
---
# <a name="porting-from-scsiport-to-storport"></a>从 ScsiPort 移植到 StorPort


以下是所需端口中基于 Scsiport 的微型端口驱动程序的示例代码，以便基于 Storport 微型端口驱动程序的迁移活动的摘要：

-   删除所有 NextRequest 和 NextLuRequest 调用

-   重命名所有 StorPortXxx ScsiPortXxx 调用

-   添加 BuildIo 例程 (移动约 75%的代码从 StartIo)

-   将驱动程序转换为全双工操作

-   添加队列管理例程 （错误处理，适配器重新启动）

-   添加了 LUN 和目标重置支持

-   添加代码以在内部分配队列标记 （硬件限制）

-   添加同步总线重置和完整适配器重启的例程

-   添加支持 SRB\_函数\_POWER （通过 SRB 适配器关闭）

-   添加 StorPortSetDeviceQueueDepth 调用-LUN 队列深度设置为 31

 

 





---
title: 容器 ID
description: 容器 ID 是系统提供的设备标识字符串，用于对与计算机上安装的单一功能或多功能设备关联的功能设备进行唯一的分组。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 898cf407cdba181de2f8664fa10274325f4a2505
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827833"
---
# <a name="container-id"></a>容器 ID


容器 ID 是系统提供的设备标识字符串，用于对与计算机上安装的单一功能或多功能设备关联的功能设备进行唯一的分组。

从 Windows 7 开始，即插即用 (PnP) 管理器使用容器 ID 对从发起并属于特定物理设备的每个实例的一个或多个设备 *)  (节点* 进行分组。 此实例称为 *设备**容器*。

将源自单个设备实例的所有 devnodes 分组可实现以下操作：

-   操作系统可以确定功能在子 devnodes 及其容器 devnode 之间的关系。

-   用户或应用程序是以设备为中心的设备视图（而不是传统的以函数为中心的视图）提供的。

本部分包含的主题更详细地介绍了容器 ID：

[容器 ID 概述](overview-of-container-ids.md)

[如何生成容器 ID](how-container-ids-are-generated.md)

[验证容器 ID 的实现](verifying-the-implementation-of-container-ids.md)

[排查容器 ID 实现问题](troubleshooting-the-implementation-of-container-ids.md)

 

 






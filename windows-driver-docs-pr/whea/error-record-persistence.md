---
title: 错误记录持久性
description: 错误记录持久性
ms.assetid: fe43f93a-59bd-4158-ad00-8fef595528cb
keywords:
- Windows 硬件错误体系结构 WDK，错误记录持久性
- WHEA WDK，错误记录持久性
- 错误 WDK WHEA，错误记录持久性
- 错误记录持久性 WDK WHEA
- 正在保存硬件错误记录 WDK WHEA
- 存储硬件错误记录 WDK WHEA
- 编写硬件错误记录 WDK WHEA
- 检索硬件错误记录 WDK WHEA
- 读取硬件错误记录 WDK WHEA
- 硬件错误 WDK WHEA，错误记录持久性
- 特定于平台的硬件错误驱动程序插件 WDK WHEA，错误记录持久性
- PSHED 插件 WDK WHEA 错误记录持久性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9af0a18c33c832d7ca393e9d7a7fbf3bfa7c0c9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547308"
---
# <a name="error-record-persistence"></a>错误记录持久性


PSHED 公开的接口允许 Windows 内核来保存和检索错误记录到或从系统的永久数据存储的操作系统。 错误的源代码管理操作包括：

-   将错误记录写入到永久性数据存储

-   从持久性数据存储中读取的错误记录

-   清除错误记录从持久性数据存储

如果硬件平台不实现硬件或固件受 PSHED 的错误记录持久性机制与兼容，平台供应商必须实现参与错误记录持久性 PSHED 插件。 与错误记录持久性机制的硬件平台实现此 PSHED 插件接口。

有关如何实现参与错误记录持久性 PSHED 插件的详细信息，请参阅[参与错误记录持久性](participating-in-error-record-persistence.md)。

有关错误记录持久性的详细信息，请参阅[错误记录持久性机制](error-record-persistence-mechanism.md)。

 

 





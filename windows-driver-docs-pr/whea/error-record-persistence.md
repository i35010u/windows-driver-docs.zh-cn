---
title: 错误记录持久性
description: 错误记录持久性
keywords:
- Windows 硬件错误体系结构 WDK，错误记录持久性
- WHEA WDK，错误记录暂留
- 错误，WDK WHEA，错误记录暂留
- 错误记录持久性 WDK WHEA
- 保存硬件错误记录 WDK WHEA
- 存储硬件错误记录 WDK WHEA
- 写入硬件错误记录 WDK WHEA
- 检索硬件错误记录 WDK WHEA
- 读取硬件错误记录 WDK WHEA
- 硬件错误 WDK WHEA，错误记录暂留
- 平台特定硬件错误驱动程序插件 WDK WHEA，错误记录暂留
- PSHED 插件 WDK WHEA，错误记录暂留
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24820190f0a4312acd3421bc486c6e95ca98cfaa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837599"
---
# <a name="error-record-persistence"></a>错误记录持久性


PSHED 向操作系统公开一个接口，该接口允许 Windows 内核在系统的永久性数据存储中保存和检索错误记录。 错误源代码管理操作包括：

-   向持久数据存储写入错误记录

-   从永久性数据存储中读取错误记录

-   从永久性数据存储中清除错误记录

如果硬件平台未实现与错误记录 PSHED 支持的持久性机制兼容的硬件或固件，则平台供应商必须实现参与错误记录持久性的 PSHED 插件。 此 PSHED 插件接口具有由硬件平台实现的错误记录持久性机制。

有关如何实现参与错误记录持久性的 PSHED 插件的详细信息，请参阅 [参与错误记录持久性](participating-in-error-record-persistence.md)。

有关错误记录持久性的详细信息，请参阅 [错误记录永久性机制](error-record-persistence-mechanism.md)。

 

 





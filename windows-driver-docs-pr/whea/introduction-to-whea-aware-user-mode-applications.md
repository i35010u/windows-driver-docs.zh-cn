---
title: WHEA 感知型用户模式应用程序简介
description: WHEA 感知型用户模式应用程序简介
keywords:
- Windows 硬件错误体系结构 WDK，用户模式应用程序
- WHEA WDK，用户模式应用程序
- 硬件错误 WDK WHEA，用户模式应用程序
- 错误 WDK WHEA，用户模式应用程序
- 用户模式应用程序 WDK WHEA
- 事件 WDK WHEA
- 事件 WDK WHEA，类别
- Windows 硬件错误体系结构 WDK，事件
- WHEA WDK，事件
- 硬件错误 WDK WHEA，事件
- 错误 WDK WHEA，事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2b128d3e0635bc66639a27559a95a5b23e18e2f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787137"
---
# <a name="introduction-to-whea-aware-user-mode-applications"></a>WHEA 感知型用户模式应用程序简介


Windows 硬件错误体系结构 (WHEA) 为用户模式应用程序提供处理 WHEA 硬件错误事件和执行 WHEA 管理操作的机制。

处理 WHEA 硬件错误事件分为两类：

<a href="" id="event-log-processing"></a>*事件日志处理*  
查询系统事件日志以检索和处理过去的 WHEA 硬件错误事件。

<a href="" id="event-notification"></a>*事件通知*  
注册 WHEA 硬件错误事件的通知，以便在出现新事件时进行处理。

WHEA 管理操作包括出于测试目的启用或禁用错误源和注入硬件错误等操作。

单用户模式应用程序可以使用事件处理和管理机制的任意组合。

WHEA 硬件错误：从 Windows Vista 开始支持处理应用程序。 有关如何实现处理 WHEA 硬件错误事件的用户模式应用程序的详细信息，请参阅 [WHEA 硬件错误事件处理应用程序](whea-hardware-error-event-processing-applications.md)。

Windows Server 2008、Windows Vista SP1 和更高版本的 Windows 支持 WHEA 管理应用程序。有关如何实现执行 WHEA 管理操作的用户模式应用程序的详细信息，请参阅 [WHEA 管理应用](whea-management-applications.md)程序。

 

 





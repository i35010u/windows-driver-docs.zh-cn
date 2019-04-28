---
title: WHEA 感知型用户模式应用程序简介
description: WHEA 感知型用户模式应用程序简介
ms.assetid: cf2de8fa-191b-4dae-aaac-5d6d74f94ca7
keywords:
- Windows 硬件错误体系结构 WDK，用户模式应用程序
- WHEA WDK，用户模式应用程序
- 硬件错误 WDK WHEA，用户模式应用程序
- 错误 WDK WHEA，用户模式应用程序
- 用户模式应用程序 WDK WHEA
- WDK WHEA 事件
- WDK WHEA，类别的事件
- Windows 硬件错误体系结构 WDK 事件
- WHEA WDK 事件
- 硬件错误 WDK WHEA，事件
- 错误 WDK WHEA，事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8aab35dafdf21cbf19fc90489f991a6773ac6897
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340780"
---
# <a name="introduction-to-whea-aware-user-mode-applications"></a>WHEA 感知型用户模式应用程序简介


Windows 硬件错误体系结构 (WHEA) 提供了用于处理 WHEA 硬件错误事件和执行 WHEA 管理操作的用户模式应用程序的机制。

WHEA 硬件错误事件的处理操作划分为两个类别：

<a href="" id="event-log-processing"></a>*事件日志处理*  
查询系统事件日志，以检索和处理过去的 WHEA 硬件错误事件。

<a href="" id="event-notification"></a>*事件通知*  
正在注册的 WHEA 硬件错误事件的通知来处理新的事件发生时。

WHEA 管理操作包括操作，例如启用或禁用错误源以及将注入以进行测试的硬件错误。

单用户模式应用程序可以使用事件处理和管理机制的任何组合。

WHEA 硬件错误事件处理应用程序支持与 Windows Vista 一起启动。 有关如何实现处理 WHEA 硬件错误事件的用户模式应用程序的详细信息，请参阅[WHEA 硬件错误的事件处理应用程序](whea-hardware-error-event-processing-applications.md)。

WHEA 管理应用程序支持在 Windows Server 2008 中，Windows Vista SP1 和更高版本的 Windows，详细了解如何实现的用户模式应用程序执行 WHEA 管理操作，请参阅[WHEA 管理应用程序](whea-management-applications.md)。

 

 





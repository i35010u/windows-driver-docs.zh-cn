---
title: 将断点用于调试器引擎 API
description: 使用断点调试器引擎 API-设置和控制
keywords:
- 调试器引擎，断点
- 断点
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ac32cf9e28081b6078653dc8d539bc259bbbeb6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803155"
---
# <a name="using-breakpoints-with-the-debugger-engine-api"></a>将断点用于调试器引擎 API


## <span id="ddk_breakpoints_dbx"></span><span id="DDK_BREAKPOINTS_DBX"></span>


断点是事件触发器，当满足断点的条件时，将暂停目标的执行并中断到调试器。 断点允许用户在执行达到某个点或访问某个内存位置时，分析和修改目标。

调试器引擎通过修改断点位置上的处理器指令，将 *软件断点* 插入目标中;此修改对引擎的客户端不可见。 当目标在断点位置执行指令时，将触发软件断点。 调试器引擎会将 *处理器断点* 插入目标的处理器;它的功能特定于处理器。 当访问断点位置的内存时，处理器会触发此方法;创建断点时，将触发此断点的访问类型。

本主题包括以下内容：

[设置断点](setting-breakpoints.md)

[控制断点标志和参数](controlling-breakpoint-flags-and-parameters.md)

 

 






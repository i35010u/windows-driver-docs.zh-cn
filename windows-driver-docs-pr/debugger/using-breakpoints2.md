---
title: 调试器引擎 API 中使用断点
description: 使用断点调试器引擎 API-设置和控制
ms.assetid: d1880895-dc01-429b-af48-762cb24539f1
keywords:
- 调试器引擎断点
- breakpoints
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0937c06b35e2c1ec52629958fd9acf194d8a2a04
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576812"
---
# <a name="using-breakpoints-with-the-debugger-engine-api"></a>调试器引擎 API 中使用断点


## <span id="ddk_breakpoints_dbx"></span><span id="DDK_BREAKPOINTS_DBX"></span>


断点是目标的事件触发器，在满足断点的条件时，将暂停执行，并进入调试器。 断点允许用户分析，并可能修改目标，当执行到达某一时间点或访问某些内存位置时。

调试器引擎将插入*软件断点*此修改为通过修改断点的位置; 的处理器指令的目标是看不到引擎的客户端。 当目标执行断点位置处的指令时，会触发软件断点。 一个*处理器断点*由调试器引擎; 插入到目标的处理器其功能是特定于处理器的。 访问断点位置处的内存; 时触发的处理器创建断点时，指定哪种类型的访问将触发此断点。

本主题包括以下内容：

[设置断点](setting-breakpoints.md)

[控制断点标志和参数](controlling-breakpoint-flags-and-parameters.md)

 

 






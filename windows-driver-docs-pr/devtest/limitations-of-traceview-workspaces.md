---
title: TraceView 工作区的限制
description: TraceView 工作区的限制
ms.assetid: 9c8cad66-251c-473e-b723-aae744b6737a
keywords:
- 工作区 WDK TraceView，限制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5045f9a2fdc006215e8639ffb79219e809459928
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369737"
---
# <a name="limitations-of-traceview-workspaces"></a>TraceView 工作区的限制


TraceView 工作区功能具有以下限制。

-   由于路径和文件名与跟踪会话保存在工作区中，在工作区中保存的文件是重用，并且覆盖每次打开工作区。 若要保留您的文件，移动或重命名它们后每个跟踪会话。

-   不会自动保存到工作区的更改和 TraceView 不会提示你保存它们。

-   无法保存的工作区包括跟踪会话组。 有关详细信息，请参阅[分组跟踪会话](grouping-trace-sessions.md)。

-   可以将只有一个跟踪会话或日志显示保存在每个工作区。 若要保存多个跟踪会话或记录显示，请创建一个跟踪会话组。

-   工作区不保存在文件中。 不能将它们移到远程计算机。

-   不可能在其他版本的 TraceView 支持一个版本的 TraceView 创建工作区的。

 

 






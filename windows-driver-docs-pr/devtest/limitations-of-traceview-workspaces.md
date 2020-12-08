---
title: TraceView 工作区的限制
description: TraceView 工作区的限制
keywords:
- 工作区 WDK TraceView，限制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 978542f30d7170b5d03d5f6d69a273e97d280d32
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795609"
---
# <a name="limitations-of-traceview-workspaces"></a>TraceView 工作区的限制


TraceView 工作区功能具有以下限制。

-   由于与跟踪会话关联的路径和文件名保存在工作区中，因此在每次打开工作区时，保存在工作区中的文件都将被重复使用并被覆盖。 若要保留文件，请在每个跟踪会话后移动或重命名文件。

-   对工作区所做的更改不会自动保存，TraceView 不会提示你保存。

-   不能保存包含跟踪会话组的工作区。 有关详细信息，请参阅对 [跟踪会话进行分组](grouping-trace-sessions.md)。

-   只能在每个工作区中保存一个跟踪会话或日志显示。 若要保存多个跟踪会话或日志显示，请创建一个跟踪会话组。

-   工作区不保存在文件中。 不能将它们移动到远程计算机。

-   在其他版本的 TraceView 中，可能不支持 TraceView 的一个版本创建的工作区。

 

 






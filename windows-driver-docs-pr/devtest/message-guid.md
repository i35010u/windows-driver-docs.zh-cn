---
title: 消息 GUID
description: 消息 GUID
ms.assetid: 3a51d730-61a4-44d9-aaf6-117736412efe
keywords:
- 消息 Guid WDK
- Guid WDK 软件跟踪
- 标识符 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb759d48be2b7aedc7bf7b5f961de876c2645ac2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564040"
---
# <a name="message-guid"></a>消息 GUID

一个*消息 GUID*，或*解码 GUID*，是从特定的提供程序分配到的跟踪消息的 GUID。 作为文件的名称的使用的同一个 GUID[跟踪消息格式 (TMF) 文件](trace-message-format-file.md)（.tmf 扩展名） 用于存储这些消息的格式设置说明。

事件跟踪 Windows (ETW) 使用消息的 GUID 将跟踪消息与正确的 TMF 文件相关联。 有关如何执行此操作的详细信息，请参阅[Tracepdb](tracepdb.md)。

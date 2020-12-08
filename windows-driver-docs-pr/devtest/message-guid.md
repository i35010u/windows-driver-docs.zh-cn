---
title: 消息 GUID
description: 消息 GUID
keywords:
- 消息 Guid WDK
- Guid WDK 软件跟踪
- 标识符 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cab9a1ec56def3d0597a2a41f5a1850e47a4d0ba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811153"
---
# <a name="message-guid"></a>消息 GUID

*消息 guid*（即 *解码 guid*）是分配给来自特定提供程序的跟踪消息的 guid。 同一 GUID 用作 [跟踪消息格式的文件名， (TMF) 文件](trace-message-format-file.md) ( 扩展) ，用于存储这些消息的格式设置说明。

Windows (ETW) 的事件跟踪使用消息 GUID 将跟踪消息与正确的 TMF 文件相关联。 有关如何执行此操作的详细信息，请参阅 [Tracepdb](tracepdb.md)。

---
title: 正在检查 IRP_MJ_FILE_SYSTEM_CONTROL Oplock 状态
description: 正在检查 IRP_MJ_FILE_SYSTEM_CONTROL 操作 Oplock 状态
ms.assetid: 3651d9ed-6b6f-4b60-9dfa-1c5c0c78b1a1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 146acf363d8c9cc363a135f88ab98efb4a69532d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324318"
---
# <a name="checking-the-oplock-state-of-irpmjfilesystemcontrol"></a>正在检查 IRP_MJ_FILE_SYSTEM_CONTROL Oplock 状态

某些 IRP_MJ_FILE_SYSTEM_CONTROL 操作检查 oplock 状态。 以下操作执行此检查：
- **FSCTL_SET_ZERO_DATA**

此信息适用于调用方想要零给定流的当前内容。

|请求类型|条件|
|---|---|
|级别 1<br>Batch<br>Filter<br>读取句柄<br>读写<br>读写句柄|上中断 IRP_MJ_FILE_SYSTEM_CONTROL （适用于 FSCTL_SET_ZERO_DATA) 时：<ul><li>该操作发生 FILE_OBJECT 具有不同 oplock 键 FILE_OBJECT 拥有 oplock。</ul></li><hr>如果 oplock 已损坏：<ul><li>为无中断</li><li>读取句柄请求：尽管需要确认该中断，则操作将继续立即 （例如，而无需等待确认）。</li><li>对于所有其他请求类型：继续操作之前必须收到确认。</li></ul>|
|Read|上中断 IRP_MJ_FILE_SYSTEM_CONTROL （适用于 FSCTL_SET_ZERO_DATA) 时：<ul><li>该操作发生 FILE_OBJECT 具有不同 oplock 键 FILE_OBJECT 拥有 oplock。</ul></li><hr>如果 oplock 已损坏：<ul><li>为无中断</li><li>不发送任何确认是必需的可以立即继续操作。</li></ul>|
|级别 2|<ul><li>为无始终中断。</li><li>不发送任何确认是必需的可以立即继续操作。</li></ul>|




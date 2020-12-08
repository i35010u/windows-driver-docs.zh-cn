---
title: 检查 IRP_MJ_LOCK_CONTROL 操作的 Oplock 状态
description: 检查 IRP_MJ_LOCK_CONTROL 操作的 Oplock 状态
ms.date: 11/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: f65a25744285e50fa83de99017cee6c9cd1e6e28
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839923"
---
# <a name="checking-the-oplock-state-of-an-irp_mj_lock_control-operation"></a>检查 IRP_MJ_LOCK_CONTROL 操作的 Oplock 状态

以下 [oplock 中断](./breaking-oplocks.md) 条件适用于给定流上的每个字节范围锁操作。

### <a name="conditions-for-a-level-2-request-type"></a>第2级请求类型的条件

- 始终中断到无。

- 不需要确认;操作会立即继续。

### <a name="conditions-for-a-filter-request-type"></a>筛选器请求类型的条件

- Oplock 不会中断。

- 不需要确认，操作会立即继续。

### <a name="conditions-for-level-1-batch-read-read-handle-read-write-and-read-write-handle-request-types"></a>级别1、批处理、读取、读取句柄、读写和读写句柄请求类型的条件

- 当锁定操作发生在具有 oplock 键的 FILE_OBJECT 上，而该操作与拥有 oplock 的 FILE_OBJECT 的键不同时，中断 IRP_MJ_LOCK_CONTROL。 如果 oplock 中断，则中断到无。

- 确认要求不同如下：

  - 读取请求：不需要确认;操作会立即继续。

  - Read-Handle 和读写句柄请求：尽管需要确认中断，但操作会立即继续 (例如，无需等待确认) 。

  - 级别1、批处理和 Read-Write 请求：必须先收到确认，然后才能继续操作。

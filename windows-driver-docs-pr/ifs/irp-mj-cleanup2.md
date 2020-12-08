---
title: 检查 IRP_MJ_CLEANUP 操作的 Oplock 状态
description: 检查 IRP_MJ_CLEANUP 操作的 Oplock 状态
ms.date: 11/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: ede96c53bc547f3ccd3ac32ea965c7c2d390411c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830535"
---
# <a name="checking-the-oplock-state-of-an-irp_mj_cleanup-operation"></a>检查 IRP_MJ_CLEANUP 操作的 Oplock 状态

以下 [oplock 中断](./breaking-oplocks.md) 条件仅适用于关闭 *流* 的时间。

### <a name="conditions-for-level-2-and-read-request-types"></a>级别2和读取请求类型的条件

- 始终中断到无。 请注意，不会影响同一流上的其他第2级或读取 oplock。只有与此 FILE_OBJECT 关联的第2级或读取 oplock 才会断开。

- 不需要确认;操作会立即继续。

### <a name="conditions-for-level-1-batch-filter-read-handle-read-write-and-read-write-handle-request-types"></a>级别1、批处理、筛选器、读取句柄、读写和读写句柄请求类型的条件

- 始终中断到无。

- 不需要确认;操作会立即继续。 请注意， (Irp) 等待来自挂起中断请求的确认的任何 i/o 操作都会立即完成。

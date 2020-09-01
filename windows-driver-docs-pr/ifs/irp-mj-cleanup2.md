---
title: 检查 IRP_MJ_CLEANUP 操作的 Oplock 状态
description: 检查 IRP_MJ_CLEANUP 操作的 Oplock 状态
ms.assetid: 5e078575-cbb8-4460-9986-4c546b8c20be
ms.date: 11/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: dab5ef00af8279d41e7b93980913b780e58f1e96
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067408"
---
# <a name="checking-the-oplock-state-of-an-irp_mj_cleanup-operation"></a>检查 IRP_MJ_CLEANUP 操作的 Oplock 状态

以下 [oplock 中断](./breaking-oplocks.md) 条件仅适用于关闭 *流* 的时间。

### <a name="conditions-for-level-2-and-read-request-types"></a>级别2和读取请求类型的条件

- 始终中断到无。 请注意，不会影响同一流上的其他第2级或读取 oplock。只有与此 FILE_OBJECT 关联的第2级或读取 oplock 才会断开。

- 不需要确认;操作会立即继续。

### <a name="conditions-for-level-1-batch-filter-read-handle-read-write-and-read-write-handle-request-types"></a>级别1、批处理、筛选器、读取句柄、读写和读写句柄请求类型的条件

- 始终中断到无。

- 不需要确认;操作会立即继续。 请注意， (Irp) 等待来自挂起中断请求的确认的任何 i/o 操作都会立即完成。
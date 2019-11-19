---
title: 检查 IRP_MJ_WRITE 操作的 Oplock 状态
description: 检查 IRP_MJ_WRITE 操作的 Oplock 状态
ms.assetid: 04d09810-f157-4140-8bfb-c780a65cdf77
ms.date: 11/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 636a394cdc3cfb216efba43bbcf6f30795bd26db
ms.sourcegitcommit: dac02b6af84c75e31038dae3fccc25f026a97758
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/19/2019
ms.locfileid: "74166139"
---
# <a name="checking-the-oplock-state-of-an-irp_mj_write-operation"></a>检查 IRP_MJ_WRITE 操作的 Oplock 状态

以下条件仅适用于正在写入*流*并且写入不是分页 i/o 的情况。

- 对于**第2级**oplock 类型，始终中断到无。 不需要确认;操作会立即继续。

- 所有其他操作锁定类型仅当在具有来自拥有 oplock 的 FILE_OBJECT 上具有不同 oplock 密钥的 FILE_OBJECT 上发生写入操作时才会 IRP_MJ_WRITE 中断。 如果 oplock 中断，则中断到无。 确认要求如下所示：

  - **读取**Oplock：不需要确认;操作会立即继续。
  
  - **读取句柄**Oplock：尽管需要确认中断，但操作会立即继续进行（例如，无需等待确认）。
  
  - **级别 1**、**批处理**、**筛选器**、**读写**和**读写句柄**oplock：必须先收到确认，然后才能继续操作。

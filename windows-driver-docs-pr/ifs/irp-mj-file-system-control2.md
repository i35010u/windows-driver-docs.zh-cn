---
title: 正在检查 Oplock 状态 IRP_MJ_FILE_SYSTEM_CONTROL
description: 检查 IRP_MJ_FILE_SYSTEM_CONTROL 操作的 Oplock 状态
ms.assetid: 3651d9ed-6b6f-4b60-9dfa-1c5c0c78b1a1
ms.date: 11/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 907018a1f5a007611cb66ee977486f372b942135
ms.sourcegitcommit: 79ff84ffc2faa5fdb3294e1fb5791f6a0ea7ef50
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/26/2019
ms.locfileid: "74543044"
---
# <a name="checking-the-oplock-state-of-irp_mj_file_system_control"></a>正在检查 Oplock 状态 IRP_MJ_FILE_SYSTEM_CONTROL

以下 IRP_MJ_FILE_SYSTEM_CONTROL 操作检查 oplock 状态：

- **FSCTL_SET_ZERO_DATA**

当调用方希望使给定流的当前内容为零时，将应用此信息。

### <a name="conditions-for-a-level-2-request-type"></a>第2级请求类型的条件：

- 始终中断到无。

- 不需要确认;操作会立即继续。

### <a name="conditions-for-all-other-request-types"></a>所有其他请求类型的条件：

- 当操作发生在带有 oplock 密钥的 FILE_OBJECT 上时中断 IRP_MJ_FILE_SYSTEM_CONTROL （对于 FSCTL_SET_ZERO_DATA），该操作与拥有 oplock 的 FILE_OBJECT 的密钥不同。 如果 oplock 中断，则中断到无。

- 确认要求不同如下：

  - 读取请求：不需要确认;操作会立即继续。
  
  - 读取句柄请求：尽管需要确认中断，但操作会立即继续进行（例如，无需等待确认）。
  
  - 级别1、批处理、筛选器、读写和读写处理请求：必须先收到确认，然后才能继续操作。

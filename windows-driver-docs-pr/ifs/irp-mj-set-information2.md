---
title: 检查 IRP_MJ_SET_INFORMATION 操作的 Oplock 状态
description: 检查 IRP_MJ_SET_INFORMATION 操作的 Oplock 状态
ms.assetid: d164be8d-cf42-4b96-9883-e0f8223bfde4
ms.date: 11/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: a32dbb85a64992efc694fae1523e5b5afb4b8955
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063056"
---
# <a name="checking-the-oplock-state-of-an-irp_mj_set_information-operation"></a>检查 IRP_MJ_SET_INFORMATION 操作的 Oplock 状态

以下 IRP_MJ_SET_INFORMATION 操作检查 oplock 状态：

- FileEndOfFileInformation
- FileAllocationInformation
- FileValidDataLengthInformation
- FileRenameInformation
- FileShortNameInformation
- FileLinkInformation
- FileDispositionInformation

## <a name="checking-oplock-state-for-fileendoffileinformation-fileallocationinformation-and-filevaliddatalengthinformation-operations"></a>正在检查 oplock 状态是否适用于 FileEndOfFileInformation、FileAllocationInformation 和 FileValidDataLengthInformation 操作

此信息适用于对文件或流执行以下操作：

- 调用方尝试更改流的逻辑大小。 请注意，当缓存管理器的惰性编写器线程尝试设置新的文件尾时，不进行任何 oplock 检查。 这是因为，在接收到实际的写入请求时，会进行此检查。

- 调用方尝试更改流的分配大小。

### <a name="conditions-for-a-level-2-request-type"></a>第2级请求类型的条件

- 始终中断到无。

- 不需要确认;操作会立即继续。

### <a name="conditions-for-all-other-request-types"></a>所有其他请求类型的条件

- 当操作发生在具有不同于拥有 oplock 的 FILE_OBJECT 的键的操作 FILE_OBJECT 上时，在 FileEndOfFileInformation、FileAllocationInformation 和) FileValidDataLengthInformation 的 IRP_MJ_SET_INFORMATION (中断。 如果 oplock 中断，则中断到无。

- 确认要求不同如下：

  - 读取请求：不需要确认;操作会立即继续。

  - 读取句柄请求：尽管需要确认中断，但操作会立即继续 (即，无需等待确认) 。

  - 级别1、批处理、筛选器、读写和读写处理请求：必须先收到确认，然后才能继续操作。

## <a name="checking-oplock-state-for-filerenameinformation-fileshortnameinformation-and-filelinkinformation-operations"></a>正在检查 oplock 状态是否适用于 FileRenameInformation、FileShortNameInformation 和 FileLinkInformation 操作

此信息适用于对文件或流执行以下操作：

- 正在重命名文件或流。

- 正在为文件设置短名称。

- 正在为文件创建硬链接。 如果新的硬链接取代了到其他文件的现有链接，并在被取代的链接上存在 oplock，则这会影响 oplock 状态。

- 正在重命名其锁定的流的祖先目录，或正在设置祖先目录的短名称。

### <a name="conditions-for-level-1-level-2-read-and-read-write-operations"></a>级别1、级别2、读取和读写操作的条件

- Oplock 不会中断。

- 不需要确认，操作会立即继续。

### <a name="conditions-for-batch-filter-read-handle-and-read-write-handle-operations"></a>批处理、筛选器、读取句柄和读写句柄操作的条件

- 当操作发生在具有不同于拥有 oplock 的 FILE_OBJECT 的键的操作 FILE_OBJECT 上时，在 FileRenameInformation、FileShortNameInformation 和) FileLinkInformation 的 IRP_MJ_SET_INFORMATION (中断。 如果 oplock 中断：

  - 批处理和筛选请求中断到无。

  - 读取-处理请求中断。

  - 读写-处理请求中断到读写。

- 必须先收到确认，然后才能继续操作。
  
## <a name="checking-oplock-state-for-filedispositioninformation-operations"></a>正在为 FileDispositionInformation 操作检查 oplock 状态

当调用方尝试删除文件时，将应用此信息。

- 当操作发生在具有 oplock 键的 FILE_OBJECT 上，而该操作与拥有 oplock 的 FILE_OBJECT 的键不同， **并且** 在 [FILE_DISPOSITION_INFORMATION](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_disposition_information)时，IRP_MJ_SET_INFORMATION (对 FileDispositionInformation) 中断。DeleteFile 是 * * TRUE * * * *。 如果 oplock 中断：

  - 读取-处理请求中断。

  - 读写-处理请求中断到读写。

- 必须先收到确认，然后才能继续操作。
---
title: 内核扩展属性
description: 筛选器管理器和微筛选器驱动程序体系结构
keywords:
- 扩展的文件属性
- 内核 EA
- 扩展特性
- $Kernel
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16b9dbe69f85ba5c1561f920803ba1a8d151c8a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841143"
---
# <a name="kernel-extended-attributes"></a>内核扩展属性
内核扩展属性（内核 EA）是在 Windows 8 中添加到 NTFS 的一项功能，可提高映像文件签名验证的性能。  验证映像签名是一种开销高昂的操作。 因此，存储有关以前已验证的二进制文件的信息是否已更改，或者是否会减少映像需要进行完整签名检查的实例数。


## <a name="overview"></a>概述
只能从内核模式修改带有名称前缀 ``$Kernel`` 的 EA。 以该字符串开头的任何 EA 都被视为内核 EA。 在检索所需的更新序列号（USN）之前，建议首先发出**FSCTL_WRITE_USN_CLOSE_RECORD** ，因为这会提交先前可能已发生的文件的任何挂起的 USN 日志更新。 如果不这样做， **FileUSN**值可能会在内核 EA 设置之后不久发生更改。

建议内核 EA 至少包含以下信息：
- USN UsnJournalID
  - **UsnJournalID**字段是一个 GUID，用于标识 USN 日志文件的当前具体化更新。  可以从每个卷的用户模式中删除和创建 USN 日志。  每次创建 USN 日志时，都会生成一个新的**UsnJournalID** GUID。  使用此字段，你可以判断是否存在禁用了 USN 日志并且可以重新验证的时间段。
    - 可以使用[FSCTL_QUERY_USN_JOURNAL](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-fsctl_query_usn_journal)检索此值。
- USN FileUSN
  - **FileUSN**值包含对文件进行的最后一次更改的 USN ID 并在给定文件的主文件表（MFT）记录内进行跟踪。
    - 删除 USN 日志时， **FileUSN**将重置为零。

然后，将此信息与任何其他的给定使用量一起设置为内核 EA。


## <a name="setting-a-kernel-extended-attribute"></a>设置内核扩展属性
若要设置内核 EA，它必须以前缀 ``"$Kernel."`` 开头，并 trailed 有效的 EA 名称字符串。 如果尝试从用户模式设置内核 EA，将被自动忽略。  请求将返回**STATUS_SUCCESS** ，但不会进行实际的 EA 修改。 若要设置从内核模式调用 API （如[ZwSetEaFile](https://msdn.microsoft.com/library/windows/hardware/ff961908)或[FltSetEaFile](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltseteafile) ）的内核 EA 是不够的。  这是因为 SMB 支持在网络中设置 EA，并将从服务器上的内核模式发出这些请求。  

若要设置内核 EA，调用方还必须在 IRP （i/o 请求数据包）的 MinorFunction 字段中设置**IRP_MN_KERNEL_CALL**值。 由于设置此字段的唯一方法是生成自定义 IRP，因此从 FsRtl 包中将例程[FsRtlSetKernelEaFile](https://msdn.microsoft.com/library/windows/hardware/mt807493)导出为设置内核 EA 的支持函数。

你不能将普通 EA 和内核 EA 的设置与[FsRtlSetKernelEaFile](https://msdn.microsoft.com/library/windows/hardware/mt807493)的同一调用混合。  如果执行此操作，操作将失败，并出现**STATUS_INTERMIXED_KERNEL_EA_OPERATION**。    设置内核 EA 不会生成**USN_REASON_EA_CHANGE**记录到 USN 日志;因此，不能在同一操作中使用内核 EA 和常规 EA。  


## <a name="querying-an-extended-attribute"></a>查询扩展属性
在用户模式下查询 EA 的在文件中会同时返回普通 EA 和内核 EA。 它们将返回到用户模式，以最大程度地减少应用程序兼容性问题。 正常的[ZwQueryEaFile](https://msdn.microsoft.com/library/windows/hardware/ff961907)和[FltQueryEaFile](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueryeafile)操作将同时从用户模式和内核模式返回普通 EA 和内核 EA。

当只有**FileObject**可用时，使用[FsRtlQueryKernelEaFile](https://msdn.microsoft.com/library/windows/hardware/mt807492)可以更方便地从内核模式查询内核 EA。


## <a name="querying-update-sequence-number-journal-information"></a>查询更新序列号日志信息
[FSCTL_QUERY_USN_JOURNAL](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-fsctl_query_usn_journal)操作需要**SE_MANAGE_VOLUME_PRIVILEGE** ，即使是从内核模式发出的，除非在 IRP 的 MinorFunction 字段中设置了**IRP_MN_KERNEL_CALL**值。 例程**FsRtlKernelFsControlFile**已从内核中的 FsRtl 包导出，以便轻松地允许内核模式组件发出此 USN 请求。

**注意**从 Windows 10 开始，版本1703及更高版本，此操作不再需要 SE_MANAGE_VOLUME_PRIVILEGE。  

## <a name="auto-deletion-of-kernel-extended-attributes"></a>自动删除内核扩展属性
只需重新扫描文件，因为更改文件的 USN ID 可能会占用大量资源，因为有许多良性原因可能会将 USN 更新发布到该文件。  为简化此操作，已将内核 EA 功能的自动删除添加到 NTFS。

由于在这种情况下不会删除所有内核 EA，因此使用的是扩展的 EA 前缀名称。  如果内核 EA 开头为： ``"$Kernel.Purge."`` 那么，如果以下任何 USN 原因写入到 USN 日志中，NTFS 就会删除该文件上存在的、符合给定命名语法的所有内核 EAs：  
- USN_REASON_DATA_OVERWRITE
- USN_REASON_DATA_EXTEND
- USN_REASON_DATA_TRUNCATION
- USN_REASON_REPARSE_POINT_CHANGE

即使在内存不足的情况下，也可以成功删除内核 EA。

## <a name="remarks"></a>备注
- 用户模式组件无法篡改内核 EA。
- 内核 EA 可以与普通 EA 位于同一文件中。


## <a name="see-also"></a>另请参阅
[FltQueryEaFile](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueryeafile)  
[FltSetEaFile](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltseteafile)  
[FSCTL_QUERY_USN_JOURNAL](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-fsctl_query_usn_journal)  
[FsRtlQueryKernelEaFile](https://msdn.microsoft.com/library/windows/hardware/mt807492)      
[FsRtlSetKernelEaFile](https://msdn.microsoft.com/library/windows/hardware/mt807493)  
[ZwQueryEaFile](https://msdn.microsoft.com/library/windows/hardware/ff961907)  
[ZwSetEaFile](https://msdn.microsoft.com/library/windows/hardware/ff961908)  

---
title: 扩展属性的内核
description: 筛选器管理器和微筛选器驱动程序体系结构
keywords:
- 扩展文件属性
- Kernel EA
- 扩展特性
- $Kernel
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cb4e1e5ad527df91273ad8b9ddaef84f0996ca1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520524"
---
# <a name="kernel-extended-attributes"></a>扩展属性的内核
内核扩展的特性 (内核 EA 的) 是作为一种方法来提高性能的图像文件签名验证添加到 Windows 8 中 NTFS 的功能。  它是代价高昂的操作来验证映像签名。 因此，有关存储信息，是否的二进制文件，以前已验证、 已更改或不会降低图像将不得不进行完整签名检查的实例数。


## <a name="overview"></a>概述
EA 具有名称前缀``$Kernel``只能从内核模式下进行修改。 此字符串开头的任何 EA 被视为内核 EA。 检索必要的更新序列号 (USN) 之前，建议**FSCTL_WRITE_USN_CLOSE_RECORD**会发出第一个，因为这会提交任何挂起的 USN 日志更新对先前可能已发生的文件。 如果没有， **FileUSN**不久前设置内核 EA 值可能会更改。

建议内核 EA 至少包含以下信息：
- USN UsnJournalID
  - **UsnJournalID**字段是一个 GUID，标识 USN 日记文件的当前发展。  USN 日志可以删除并创建从每个卷的用户模式。  每次 USN 日志创建一个新**UsnJournalID**将生成的 GUID。  使用此字段中，你可以判断是否有一段时间内 USN 日志被禁用，并可以重新验证。
    - 可以使用检索该值[FSCTL_QUERY_USN_JOURNAL](https://msdn.microsoft.com/library/windows/desktop/aa364583)。
- USN FileUSN
  - **FileUSN**值包含对文件进行和跟踪在给定的文件的主文件表 (MFT) 记录内的最后一个更改的 USN ID。
    - 当删除 USN 日志时， **FileUSN**重置为零。

此信息，以及任何其他可能需要给定的使用情况，则将设置该文件为内核 EA。


## <a name="setting-a-kernel-extended-attribute"></a>设置扩展属性的内核
若要设置内核 EA，则它必须以前缀开头``"$Kernel."``和尾随的是有效的 EA 名称字符串。 将以无提示方式忽略尝试从用户模式下设置内核 EA。  请求将返回**STATUS_SUCCESS**但不能进行任何实际的 EA 修改。 若要设置调用 API，例如内核 EA [ZwSetEaFile](https://msdn.microsoft.com/library/windows/hardware/ff961908)或[FltSetEaFile](https://msdn.microsoft.com/library/windows/hardware/ff544500)从内核模式不足够。  这是因为 SMB 支持 EA 的整个网络的设置，并从服务器上的内核模式发出这些请求。  

若要设置内核 EA 调用方必须也设置**IRP_MN_KERNEL_CALL** IRP （I/O 请求数据包） 的 MinorFunction 字段中的值。 由于将此字段设置的唯一方法是通过生成自定义 IRP，例程[FsRtlSetKernelEaFile](https://msdn.microsoft.com/library/windows/hardware/mt807493)作为支持函数来设置内核 EA 导出从 FsRtl 包。

不可能会互相混合的正常和内核 EA 的同一调用中设置到[FsRtlSetKernelEaFile](https://msdn.microsoft.com/library/windows/hardware/mt807493)。  如果执行此操作将失败， **STATUS_INTERMIXED_KERNEL_EA_OPERATION**。    设置将不会生成内核 EA **USN_REASON_EA_CHANGE** USN 日志; 因此记录，内核 EA 和常规 EA 不能用于相同的操作。  


## <a name="querying-an-extended-attribute"></a>查询的扩展的属性
查询从用户模式下的文件上的 EA 将返回这两个正常和内核 EA。 它们将返回到用户模式，以最大程度减少任何应用程序兼容性问题。 法线[ZwQueryEaFile](https://msdn.microsoft.com/library/windows/hardware/ff961907)并[FltQueryEaFile](https://msdn.microsoft.com/library/windows/hardware/ff543435)操作将返回正常和内核 EA 的用户和内核模式。

当仅**的文件对象**，则使用[FsRtlQueryKernelEaFile](https://msdn.microsoft.com/library/windows/hardware/mt807492)可能会更方便使用内核 EA 查询从内核模式。


## <a name="querying-update-sequence-number-journal-information"></a>查询更新序列号日志信息
[FSCTL_QUERY_USN_JOURNAL](https://msdn.microsoft.com/library/windows/desktop/aa364583)操作要求**SE_MANAGE_VOLUME_PRIVILEGE**即使发出从内核模式，除非**IRP_MN_KERNEL_CALL**设置值IRP MinorFunction 字段。 例程**FsRtlKernelFsControlFile**已从内核以轻松地使内核模式组件，发出此 USN 请求中的 FsRtl 包中导出。

**请注意**不再与 Windows 10，版本 1703年及更高版本中开始此操作需要 SE_MANAGE_VOLUME_PRIVILEGE。  

## <a name="auto-deletion-of-kernel-extended-attributes"></a>自动删除内核的扩展属性
只需重新扫描文件，因为文件已更改的 USN ID 可能很昂贵，因为有良性的原因有很多 USN 更新可能会发布到该文件。  若要简化此操作，内核 EA 功能自动删除已添加到 NTFS。

因为并非所有内核 EA 可能都想要删除在此方案中，使用扩展的 EA 前缀名称。  如果内核 EA 以开始：``"$Kernel.Purge."``然后 NTFS USN 由于以下原因的任何写入 USN 日志中，如果将删除对给定的命名语法符合该文件存在的所有内核 EAs:  
- USN_REASON_DATA_OVERWRITE
- USN_REASON_DATA_EXTEND
- USN_REASON_DATA_TRUNCATION
- USN_REASON_REPARSE_POINT_CHANGE

此删除内核 EA 会成功甚至在内存不足的情况。

## <a name="remarks"></a>备注
- 不能由用户模式组件篡改内核 EA。
- 内核 EA 可以位于与正常 EA 相同的文件。


## <a name="see-also"></a>另请参阅
[FltQueryEaFile](https://msdn.microsoft.com/library/windows/hardware/ff543435)  
[FltSetEaFile](https://msdn.microsoft.com/library/windows/hardware/ff544500)  
[FSCTL_QUERY_USN_JOURNAL](https://msdn.microsoft.com/library/windows/desktop/aa364583)  
[FsRtlQueryKernelEaFile](https://msdn.microsoft.com/library/windows/hardware/mt807492)      
[FsRtlSetKernelEaFile](https://msdn.microsoft.com/library/windows/hardware/mt807493)  
[ZwQueryEaFile](https://msdn.microsoft.com/library/windows/hardware/ff961907)  
[ZwSetEaFile](https://msdn.microsoft.com/library/windows/hardware/ff961908)  

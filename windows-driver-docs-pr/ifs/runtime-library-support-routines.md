---
title: 运行时库支持例程
description: 运行时库支持例程
ms.assetid: e333a222-32c0-46e7-a0b8-42287e19372d
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: b4c20fac746e3d55374ec6039a52907878281095
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955803"
---
# <a name="runtime-library-support-routines"></a>运行时库支持例程

下表列出了系统提供的运行时库支持例程的子集，这些例程可由内核模式文件系统和微筛选器和旧筛选器驱动程序（而不是设备驱动程序）使用。

除了此处所述的例程，文件系统和筛选器驱动程序还可以调用*ntifs*中声明的内核模式驱动程序体系结构参考部分中所述的任何**Rtl**_Xxx_例程。

**头文件：** *ntifs*

**Prefix：Rtl @ no__t-0_Xxx_

| 函数或宏 | 描述 |
| ----------------- | ----------- |
| **RtlAbsoluteToSelfRelativeSD** | 使用以绝对格式作为模板的安全描述符，以自相关格式创建新的安全描述符。 |
| **RtlAddAccessAllowedAce** | 将访问允许的访问控制项（ACE）添加到访问控制列表（ACL）。 将访问权限授予指定的安全标识符（SID）。 |
| **RtlAddAccessAllowedAceEx** | 使用继承 ACE 标志向访问控制列表（ACL）添加访问允许的访问控制项（ACE）。 将访问权限授予指定的安全标识符（SID）。 |
| **RtlAddAce** | 将一个或多个访问控制项（Ace）添加到指定的访问控制列表（ACL）。 |
| **RtlAllocateAndInitializeSid** | 保留供系统使用。 |
| **RtlAllocateHeap** | 从堆中分配内存块。 |
| **RtlAppendStringToString** | 连接两个计数字符串。 它将源中的字节复制到目标缓冲区的长度。 |
| **RtlCaptureContext** | 在调用方的上下文中检索上下文记录。 |
| **RtlCaptureStackBackTrace** | 通过遍历堆栈并记录每个帧的信息来捕获堆栈后退跟踪。 |
| **RtlCompareMemoryUlong** | 返回内存块中匹配指定模式的字节数。 |
| **RtlCompressBuffer** | 压缩缓冲区并可由文件系统驱动程序用来简化文件压缩的实现。 |
| **RtlCompressChunks** | 保留供系统使用。 |
| **RtlConvertSidToUnicodeString** | 生成安全标识符（SID）的可打印 Unicode 字符串表示形式。 |
| **RtlCopyLuid** | 将本地唯一标识符（LUID）复制到缓冲区。 |
| **RtlCopySid** | 将安全标识符（SID）的值复制到缓冲区。 |
| **RtlCreateAcl** | 创建并初始化访问控制列表（ACL）。 |
| **RtlCreateHeap** | 创建可由调用进程使用的堆对象。 此例程在进程的虚拟地址空间中保留空间，并为此块的指定初始部分分配物理存储空间。 |
| **RtlCreateSecurityDescriptorRelative** | 以自相关格式初始化新的安全描述符。 返回时，将初始化安全描述符，其中没有系统 ACL （SACL），无随机 ACL （DACL），无所有者，无主组，且所有控制标志均设置为零。 |
| **RtlCreateSystemVolumeInformationFolder** | 验证文件系统卷上是否存在 "系统卷信息" 文件夹。 如果该文件夹不存在，则创建该文件夹。 |
| **RtlCreateUnicodeString** | 创建新的计数 Unicode 字符串。 |
| **RtlCustomCPToUnicodeN** | 保留供系统使用。 |
| **RtlDecompressBuffer** | 解压缩整个压缩缓冲区。 |
| **RtlDecompressBufferEx** | 解压缩整个压缩缓冲区。 |
| **RtlDecompressBufferEx2** | 如果可能，请使用多个处理器解压缩整个压缩缓冲区。 仅为内核模式调用方实现多处理器支持。 |
| **RtlDecompressChunks** | 保留供系统使用。 |
| **RtlDecompressFragment** | 解压缩压缩缓冲区的一部分（即缓冲区 "片段"）。 |
| **RtlDecompressFragmentEx** | 尽可能使用多个处理器解压缩压缩缓冲区的一部分（即缓冲区 "片段"）。 |
| **RtlDelete** | 从显示链接树中删除指定的节点。 |
| **RtlDeleteAce** | 删除指定访问控制列表（ACL）中的访问控制项（ACE）。 |
| **RtlDeleteNoSplay** | 从显示链接树中删除指定的节点。 |
| **RtlDeleteElementGenericTable** | 从泛型表中删除元素。 |
| **RtlDeleteElementGenericTableAvl** | 从泛型表中删除元素。 |
| **RtlDescribeChunk** | 保留供系统使用。 |
| **RtlDestroyHeap** | 销毁指定的堆对象。 | \* * RtlDestroyHeap 解除和释放专用堆对象的所有页，并使堆的句柄失效。 |
| **RtlDowncaseUnicodeString** | 将指定的 Unicode 源字符串转换为小写。 转换符合当前的系统区域设置信息。 |
| **RtlEnumerateGenericTable** | 枚举泛型表中的元素。 |
| **RtlEnumerateGenericTableAvl** | 枚举泛型表中的元素。 |
| **RtlEnumerateGenericTableLikeADirectory** | 按排序规则顺序逐个返回泛型表的元素。 |
| **RtlEnumerateGenericTableWithoutSplaying** | 枚举泛型表中的元素。 |
| **RtlEnumerateGenericTableWithoutSplayingAvl** | 枚举泛型表中的元素。 |
| **RtlEqualPrefixSid** | 确定两个安全标识符（SID）前缀是否相等。 SID 前缀是整个 SID，最后一个 subauthority 值除外。 |
| **RtlEqualSid** | 确定两个安全标识符（SID）值是否相等。 两个 Sid 必须完全匹配才能视为相等。 |
| **RtlFillMemoryUlong** | 使用一个或多个 ULONG 值重复来填充指定范围的内存。 |
| **RtlFillMemoryUlonglong** | 使用给定 ULONGLONG 值的一个或多个重复项填充给定范围的内存。 |
| **RtlFindUnicodePrefix** | 在前缀表中搜索给定 Unicode 文件名的最佳匹配项。 |
| **RtlFreeHeap** | 释放由**RtlAllocateHeap**从堆中分配的内存块。 |
| **RtlFreeOemString** | 释放由任意 Rtl 所分配的存储。 **ToOemString**例程。 |
| **RtlFreeSid** | 保留供系统使用。 |
| **RtlGenerate8dot3Name** | 为指定的长文件名生成短（8.3）名称。 |
| **RtlGetAce** | 获取指向访问控制列表（ACL）中的访问控制项（ACE）的指针。 |
| **RtlGetCompressionWorkSpaceSize** | 确定**RtlCompressBuffer**和**RtlDecompressFragment**函数的工作区缓冲区的正确大小。 |
| **RtlGetDaclSecurityDescriptor** | 返回一个指针，该指针指向安全描述符的自由 ACL （DACL）。 |
| **RtlGetElementGenericTable** | 返回一个指向特定泛型表元素的调用方提供的数据的指针。 |
| **RtlGetElementGenericTableAvl** | 返回一个指针，该指针指向特定泛型 Adelson/Landis （AVL） table 元素的调用方提供的数据。 |
| **RtlGetGroupSecurityDescriptor** | 返回给定安全描述符的主要组信息。 |
| **RtlGetOwnerSecurityDescriptor** | 返回给定安全描述符的所有者信息。 |
| **RtlGetSaclSecurityDescriptor** | 返回一个指针，该指针指向安全描述符的系统 ACL （SACL）。 |
| **RtlIdentifierAuthoritySid** | 保留供系统使用。 |
| **RtlInitCodePageTable** | 保留供系统使用。 |
| **RtlInitializeGenericTable** | 初始化泛型表。 |
| **RtlInitializeGenericTableAvl** | 使用 Adelson-Velsky/Landis （AVL）树初始化泛型表。 |
| **RtlInitializeSid** | 初始化安全标识符（SID）结构。 |
| **RtlInitializeSidEx** | 初始化预先分配的安全标识符（SID）结构。 |
| **RtlInitializeSplayLinks** | 初始化显示链接节点。 |
| **RtlInitializeUnicodePrefix** | 初始化前缀表。 |
| **RtlInsertAsLeftChild** | 将显示链接节点作为指定节点的左侧子节点插入到树中。 |
| **RtlInsertAsRightChild** | 将给定的显示链接插入树中的给定节点的右侧子树。 |
| **RtlInsertElementGenericTable** | 将新元素添加到泛型表中。 |
| **RtlInsertElementGenericTableAvl** | 向泛型表中添加新项。 |
| **RtlInsertElementGenericTableFullAvl** | 向泛型表中添加新项。 |
| **RtlInsertUnicodePrefix** | 将新元素插入到 Unicode 前缀表中。 |
| **RtlIsGenericTableEmpty** | 确定泛型表是否为空。 |
| **RtlIsGenericTableEmptyAvl** | 确定泛型表是否为空。 |
| **RtlIsLeftChild** | 确定给定显示链接是否为显示链接树中节点的左侧子节点。 |
| **RtlIsNameLegalDOS8Dot3** | 确定给定的名称是否表示有效的短（8.3）文件名。 |
| **RtlIsRightChild** | 确定给定的显示链接是否是显示链接树中节点的右子。 |
| **RtlIsRoot** | 确定指定的节点是否为显示链接树的根节点。 |
| **RtlIsValidOemCharacter** | 确定指定的 Unicode 字符是否可以映射到有效的 OEM 字符。 |
| **RtlLeftChild** | 返回指向指定的显示链接节点的左侧子的指针。 |
| **RtlLengthRequiredSid** | 返回存储具有指定 subauthorities 数的安全标识符（SID）所需的缓冲区的长度（以字节为单位）。 |
| **RtlLengthSid** | 返回有效安全标识符（SID）的长度（以字节为单位）。 |
| **RtlLookupElementGenericTable** | 在泛型表中搜索与指定数据相匹配的元素。 |
| **RtlLookupElementGenericTableAvl** | 在泛型表中搜索与指定数据相匹配的元素。 |
| **RtlLookupElementGenericTableFullAvl** | 在泛型表中搜索与指定数据相匹配的元素。 |
| **RtlLookupFirstMatchingElementGenericTableAvl** | 查找树中与指示的数据匹配的最左侧元素。 |
| **RtlMultiByteToUnicodeN** | 使用当前系统 ANSI 代码页（ACP）将指定的源字符串转换为 Unicode 字符串。 源字符串不一定来自多字节字符集。 |
| **RtlMultiByteToUnicodeSize** | 确定为指定的源字符串存储 Unicode 转换所需的字节数。 假定转换使用当前系统 ANSI 代码页（ACP）。 源字符串不一定来自多字节字符集。 |
| **RtlNextUnicodePrefix** | 枚举 Unicode 前缀表中的元素。 |
| **RtlNtStatusToDosError** | 将指定的 NTSTATUS 代码转换为其等效的系统错误代码。 |
| **RtlNtStatusToDosErrorNoTeb** | 保留供系统使用。 |
| **RtlNumberGenericTableElements** | 返回泛型表中元素的数目。 |
| **RtlNumberGenericTableElementsAvl** | 返回泛型表中元素的数目。 |
| **RtlOemStringToCountedUnicodeSize** | 确定在将给定的 OEM 字符串转换为计数的 Unicode 字符串后，该字符串的大小（以字节为单位）。 |
| **RtlOemStringToCountedUnicodeString** | 使用当前系统 OEM 代码页将指定的源字符串转换为 Unicode 字符串。 |
| **RtlOemStringToUnicodeSize** | 确定在将给定的 OEM 字符串转换为以 null 结尾的 Unicode 字符串后，该字符串的大小（以字节为单位）。 |
| **RtlxOemStringToUnicodeSize** | 保留供系统使用。 |
| **RtlOemStringToUnicodeString** | 使用当前系统 OEM 代码页将给定的源字符串转换为以 null 结尾的 Unicode 字符串。 |
| **RtlOemToUnicodeN** | 使用当前系统 OEM 代码页将指定的源字符串转换为 Unicode 字符串。 |
| **RtlOffsetToPointer** | 返回给定基址中给定偏移量的指针。 |
| **RtlParent** | 返回指向显示链接树中指定节点的父节点的指针。 |
| **RtlPointerToOffset** | 返回给定指针的给定基址的偏移量。 |
| **RtlRandom** | 返回从给定种子值生成的随机数。 |
| **RtlRandomEx** | 返回从给定种子值生成的随机数。 |
| **RtlRealPredecessor** | 返回指向显示链接树中指定节点的前置任务的指针。 |
| **RtlRealSuccessor** | 返回指向显示链接树中指定节点的后续项的指针。 |
| **RtlRemoveUnicodePrefix** | 从前缀表中删除元素。 |
| **RtlReserveChunk** | 保留供系统使用。 |
| **RtlRightChild** | 返回指向指定显示链接节点的右子的指针。 |
| **RtlSecondsSince1970ToTime** | 将从1970开始到绝对系统时间值以来经过的时间（以秒为单位）。 |
| **RtlSecondsSince1980ToTime** | 将从1980开始到绝对系统时间值以来经过的时间（以秒为单位）。 |
| **RtlSelfRelativeToAbsoluteSD** | 使用以自相关格式作为模板的安全描述符，以绝对格式创建新的安全描述符。 |
| **RtlSetGroupSecurityDescriptor** | 设置绝对格式安全描述符的主要组信息。 它将替换安全描述符中已经存在的任何主组信息。 |
| **RtlSetOwnerSecurityDescriptor** | 设置绝对格式安全描述符的所有者信息。 它替换已存在于安全描述符中的所有所有者信息。 |
| **RtlSplay** | 间重新平衡或 "splays"，它是围绕指定显示链接的显示链接树，使其链接到树的新根目录。 |
| **RtlSubAuthorityCountSid** | 保留供系统使用。 |
| **RtlSubAuthoritySid** | 返回一个指针，该指针指向安全标识符（SID）的指定 subauthority。 |
| **RtlSubtreePredecessor** | 返回一个指针，该指针指向位于该节点的子树中指定节点的前置任务。 |
| **RtlSubtreeSuccessor** | 返回一个指针，该指针指向位于该节点的子树内的指定节点的后续任务。 |
| **RtlTimeToSecondsSince1970** | 将给定的绝对系统时间值转换为自1970开始后经过的时间（以秒为单位）。 |
| **RtlTimeToSecondsSince1980** | 将给定的绝对系统时间值转换为自1980开始后经过的时间（以秒为单位）。 |
| **RtlUnicodeStringToAnsiSize** | 确定存储指定 Unicode 字符串的 ANSI 转换所需的字节数。 |
| **RtlUnicodeStringToCountedOemString** | 使用当前系统 OEM 代码页将指定的 Unicode 源字符串转换为计数的 OEM 字符串。 |
| **RtlUnicodeStringToOemSize** | 确定将给定 Unicode 字符串转换为 OEM 字符串后该字符串的大小（以字节为单位）。 |
| **RtlUnicodeStringToOemSize** | 保留供系统使用。 |
| **RtlUnicodeStringToOemString** | 使用当前系统 OEM 代码页将给定的 Unicode 源字符串转换为 OEM 字符串。 |
| **RtlUnicodeToCustomCPN** | 保留供系统使用。 |
| **RtlUnicodeToMultiByteN** | 使用当前系统 ANSI 代码页（ACP）将指定的 Unicode 字符串转换为新的字符串。 转换后的字符串不必是多字节字符集。 |
| **RtlUnicodeToMultiByteSize** | 确定存储指定 Unicode 字符串的多字节转换所需的字节数。 假定转换使用当前系统 ANSI 代码页（ACP）。 |
| **RtlUnicodeToOemN** | 使用当前系统 OEM 代码页将给定的 Unicode 字符串转换为 OEM 字符串。 |
| **RtlUpcaseUnicodeStringToCountedOemString** | 使用当前系统 OEM 代码页将给定的 Unicode 源字符串转换为大写字母的 OEM 字符串。 |
| **RtlUpcaseUnicodeStringToOemString** | 使用当前系统 OEM 代码页将给定的 Unicode 源字符串转换为大写 OEM 字符串。 |
| **RtlUpcaseUnicodeToCustomCPN** | 保留供系统使用。 |
| **RtlUpcaseUnicodeToMultiByteN** | 使用当前系统 ANSI 代码页（ACP）将指定的 Unicode 字符串转换为一个大写字符的新字符串。 转换后的字符串不必是多字节字符集。 |
| **RtlUpcaseUnicodeToOemN** | 使用当前系统 OEM 代码页将给定 Unicode 字符串转换为大写 OEM 字符串。 |
| **RtlValidSid** | 验证安全标识符（SID），方法是验证修订号在已知范围内并且 subauthorities 数小于最大值。 |

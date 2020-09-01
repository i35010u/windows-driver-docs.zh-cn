---
title: 两种 I/O 操作都不是
description: 两种 I/O 操作都不是
ms.assetid: c8fc4742-e220-45c4-9113-ec5658bc09cc
keywords:
- 安全 WDK 文件系统，语义模型检查
- 语义模型检查 WDK 文件系统，i/o 操作都不是
- I/o WDK 文件系统
- i/o 操作 WDK 文件系统都不是
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bac5c73f36c64cb50c6a5591692abdecae91ba1
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064984"
---
# <a name="neither-io-operations"></a>两种 I/O 操作都不是


## <span id="ddk_neither_i_o_operations_if"></span><span id="DDK_NEITHER_I_O_OPERATIONS_IF"></span>


文件系统必须处理通常涉及直接操作用户缓冲区的操作。 此类操作在本质上是危险的，因为用户地址可能无效。 文件系统必须特别关心此类操作，并确保它们进行相应的保护。 以下操作依赖于文件系统的设备对象的 **Flags** 成员来指定 i/o 管理器如何在用户和内核地址空间之间传输数据：

-   [**IRP \_ MJ \_ 目录 \_ 控件**](./irp-mj-directory-control.md)

-   [**IRP \_ MJ \_ 查询 \_ EA**](./irp-mj-query-ea.md)

-   [**IRP \_ MJ \_ 查询 \_ 配额**](./irp-mj-query-quota.md)

-   [**IRP \_ MJ \_ 读取**](./irp-mj-read.md)

-   [**IRP \_ MJ \_ 设置 \_ EA**](./irp-mj-set-ea.md)

-   [**IRP \_ MJ \_ 设置 \_ 配额**](./irp-mj-set-quota.md)

-   [**IRP \_ MJ \_ 写入**](./irp-mj-write.md)

通常，文件系统不通过 \_ \_ \_ \_ 在其创建的卷设备对象的 **FLAGS** 成员中设置 "执行直接 IO" 和 "缓冲 IO" 来隐式选择 i/o。

以下操作将忽略文件系统设备对象的 **标志** 成员，并使用 i/o 在用户和内核地址空间之间传输数据：

-   [**IRP \_ MJ \_ 查询 \_ 安全性**](./irp-mj-query-security.md)

如果使用的不是 i/o，则文件系统负责处理其自己的数据传输操作。 这允许文件系统通过将数据直接放入应用程序的用户空间缓冲区来满足操作。 这样，文件系统必须确保用户的缓冲区在操作开始时有效，并在操作正在进行时适当地处理缓冲区无效。 Fast i/o 还传递原始指针。 开发人员应注意到，在操作开始时检查缓冲区的有效性是否不足以确保它在整个操作过程中保持有效。 例如，恶意应用程序可能会将内存块映射到部分 (例如) 、发出 i/o 操作，并在 i/o 操作正在进行时取消映射内存块。

文件系统通过多种方式来处理这种情况。 一种机制是锁定与用户地址相对应的物理内存，并在操作系统的地址空间中创建第二个映射。 这可确保文件系统使用它控制的虚拟地址。 因此，即使用户地址变为无效，文件系统创建的地址仍有效。 FASTFAT 文件系统代码使用两个不同的函数来实现此目的。 第一个函数会锁定用户缓冲区：

```cpp
VOID
FatLockUserBuffer (
    IN PIRP_CONTEXT IrpContext,
    IN OUT PIRP Irp,
    IN LOCK_OPERATION Operation,
    IN ULONG BufferLength
    )

/*++
Routine Description:

    This routine locks the specified buffer for the specified type of
    access. The file system requires this routine because it does not
    ask the I/O system to lock its buffers for direct I/O. This routine
    can only be called from the file system driver (FSD) while still in the user context.

    Note that this is the *input/output* buffer.

Arguments:
    Irp - Pointer to the Irp for which the buffer will be locked.
    Operation - IoWriteAccess for read operations, or IoReadAccess for
                write operations.
    BufferLength - Length of user buffer.

Return Value:
    None
--*/

{
    PMDL Mdl = NULL;

    if (Irp->MdlAddress == NULL) {
        //
        // Allocate the Mdl and Raise if the allocation fails.
        //
        Mdl = IoAllocateMdl( Irp->UserBuffer, BufferLength, FALSE, FALSE, Irp );
        if (Mdl == NULL) {
            FatRaiseStatus( IrpContext, STATUS_INSUFFICIENT_RESOURCES );
        }

        //
        // now probe the buffer described by the Irp. If there is an exception,
        // deallocate the Mdl and return the appropriate "expected" status.
        //
        try {
            MmProbeAndLockPages( Mdl,
                                 Irp->RequestorMode,
                                 Operation );
        } except(EXCEPTION_EXECUTE_HANDLER) {
            NTSTATUS Status;
            Status = GetExceptionCode();
            IoFreeMdl( Mdl );
            Irp->MdlAddress = NULL;
            FatRaiseStatus( IrpContext,
                            FsRtlIsNtstatusExpected(Status) ? Status : STATUS_INVALID_USER_BUFFER );
        }
    }

    UNREFERENCED_PARAMETER( IrpContext );
}
```

此例程确保当操作正在进行时，将不会在任何其他目的中重复使用为用户地址提供支持的物理内存。 为了满足非缓存用户 i/o 的需要，文件系统可能会执行此操作以将 i/o 操作发送到基础卷管理或磁盘类层。 在这种情况下，文件系统不需要将其自己的虚拟地址用于缓冲区。 第二个函数创建文件系统到内核地址空间的映射：

```cpp
PVOID
FatMapUserBuffer (
    IN PIRP_CONTEXT IrpContext,
    IN OUT PIRP Irp
    )
/*++
Routine Description:
    This routine conditionally maps the user buffer for the current I/O
    request in the specified mode. If the buffer is already mapped, it
    just returns its address.
 
    Note that this is the *input/output* buffer.

Arguments:
    Irp - Pointer to the Irp for the request.

Return Value:
    Mapped address
--*/
{
    UNREFERENCED_PARAMETER( IrpContext );

    //
    // If there is no Mdl, then we must be in  the FSD, and can simply
    // return the UserBuffer field from the Irp.
    //
    if (Irp->MdlAddress == NULL) {
        return Irp->UserBuffer;
    } else {
        PVOID Address = MmGetSystemAddressForMdlSafe( Irp->MdlAddress, NormalPagePriority );
        if (Address == NULL) {
            ExRaiseStatus( STATUS_INSUFFICIENT_RESOURCES );
        }
        return Address;
    }
}
```

FASTFAT 实现还允许第二个例程返回用户级地址，这要求 FAT 文件系统确保返回 (用户或内核) 返回的地址必须有效。 它通过使用 \_ \_ try \_ \_ 关键字和 except 关键字来创建受保护的块。

这些例程位于 WDK 包含的 fastfat 示例的 deviosup 源文件中。

如果调用方的上下文中未满足请求，则会出现另一个严重问题。 如果文件系统向工作线程发送请求，则驱动程序必须使用 MDL 锁定缓冲区，才能不会失去跟踪。 Fastfat 示例的 workque 源文件中的 **FatPrePostIrp** 函数提供了一个示例，说明如何通过 fastfat 文件系统处理此问题。

FASTFAT 文件系统使用这些例程防止范围广泛的故障，而不只是无效的用户缓冲区。 虽然这是一种非常强大的技术，但它还涉及确保所有受保护的代码块正确释放它们可能持有的任何资源。 要释放的资源包括内存、同步对象或文件系统本身的某个其他资源。 如果执行此操作，则攻击者可能会通过多次重复调用操作系统来耗尽资源来导致资源不足。

 


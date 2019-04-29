---
title: 两种 I/O 操作都不是
description: 两种 I/O 操作都不是
ms.assetid: c8fc4742-e220-45c4-9113-ec5658bc09cc
keywords:
- 安全 WDK 文件系统，语义模型检查
- 语义模型检查 WDK 的文件系统，都不 I/O 操作
- I/O WDK 的文件系统
- 既不 I/O 操作 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a58f9e6cae93e83d48a09c282cd7c003216800f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379461"
---
# <a name="neither-io-operations"></a>两种 I/O 操作都不是


## <span id="ddk_neither_i_o_operations_if"></span><span id="DDK_NEITHER_I_O_OPERATIONS_IF"></span>


文件系统必须处理通常涉及到直接操作用户缓冲区的操作。 此类操作存在固有的风险，因为用户地址可能无效。 文件系统必须特别有意识的此类操作，并确保它们适当保护，它们。 依赖于以下操作**标志**文件系统的设备对象的成员才能指定用户和内核地址空间之间传输数据 I/O 管理器的方式：

-   [**IRP\_MJ\_DIRECTORY\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff548658)

-   [**IRP\_MJ\_查询\_EA**](https://msdn.microsoft.com/library/windows/hardware/ff549279)

-   [**IRP\_MJ\_查询\_配额**](https://msdn.microsoft.com/library/windows/hardware/ff549293)

-   [**IRP\_MJ\_READ**](https://msdn.microsoft.com/library/windows/hardware/ff549327)

-   [**IRP\_MJ\_SET\_EA**](https://msdn.microsoft.com/library/windows/hardware/ff549346)

-   [**IRP\_MJ\_SET\_QUOTA**](https://msdn.microsoft.com/library/windows/hardware/ff549401)

-   [**IRP\_MJ\_WRITE**](https://msdn.microsoft.com/library/windows/hardware/ff549427)

通常情况下，文件系统选择都不 I/O 隐式设置都不执行操作\_直接\_IO 也不执行\_缓冲\_中的 IO**标志**卷设备的成员对象它创建。

以下操作将忽略**标志**文件系统的成员的设备对象，并使用任一 I/O 用户和内核地址空间之间传输数据：

-   [**IRP\_MJ\_QUERY\_SECURITY**](https://msdn.microsoft.com/library/windows/hardware/ff549298)

使用任一 I/O，文件系统是负责处理其自己的数据传输操作。 这允许文件系统，以满足操作，直接将数据放入应用程序的用户空间缓冲区。 因此，文件系统必须确保用户的缓冲区无效时该操作开始，并适当地处理正在进行操作时变为无效的缓冲区。 快速的 i/o 操作还会传递原始指针。 开发人员应注意，检查操作的开始处的缓冲区的有效性并不足以确保其保持在操作中将有效。 例如，恶意应用程序无法地图 （通过用于示例的节） 的内存块，请发出 I/O 操作，并取消映射的内存块的正在进行 I/O 操作时。

有几种方法来处理这种情况下的文件系统。 一种机制是锁定用户的地址对应的物理内存和操作系统的地址空间中创建第二个映射。 这可确保文件系统，使用它控制的虚拟地址。 因此即使用户地址变为无效，文件系统创建的地址会保持有效。 FASTFAT 文件系统代码使用两个不同的函数来实现此目的。 第一个函数锁定用户的缓冲区：

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

此例程可确保，正在进行操作时，将用户的地址的物理内存不将重用用于任何其他用途。 文件系统可能会执行此操作以发送到基础卷管理或磁盘类层来满足非缓存用户 I/O 的 I/O 操作中。 在这种情况下，文件系统不需要自己的缓冲区的虚拟地址。 第二个函数将创建文件系统映射到内核地址空间：

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

FASTFAT 实现允许将第二个例程，以返回用户级地址，这要求 FAT 文件系统，确保返回的地址 （用户或内核） 必须是有效。 这是通过使用\_\_尝试并\_ \_except 关键字创建的受保护的块。

这些例程是从 WDK 包含 fastfat 示例 deviosup.c 源文件中。

在调用方的上下文中不满足请求时，会出现另一个关键问题。 如果文件系统发布到工作线程请求，该驱动程序必须锁定具有以不会丢失对它的跟踪 MDL 缓冲区。 **FatPrePostIrp** workque.c 源文件从 fastfat 示例中的函数提供了此问题由 FASTFAT 文件系统的处理方式的示例。

FASTFAT 文件系统可防止范围广泛的故障，不只是无效用户缓冲区，使用这些例程。 虽然这是很强大的技术，它还涉及到确保所有受保护的代码块正确释放它们可能持有的资源。 若要释放的资源包括内存、 同步对象或文件系统本身的一些其他资源。 如果不这样做会使潜在的攻击者能够许多重复调用到操作系统耗尽资源，从而导致资源不足。

 

 





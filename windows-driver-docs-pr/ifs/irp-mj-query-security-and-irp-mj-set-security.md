---
title: IRP_MJ_QUERY_SECURITY 和 IRP_MJ_SET_SECURITY
description: IRP_MJ_QUERY_SECURITY 和 IRP_MJ_SET_SECURITY
keywords:
- IRP_MJ_QUERY_SECURITY
- IRP_MJ_SET_SECURITY
- 安全 WDK 文件系统，添加安全检查
- 安全检查 WDK 文件系统，IRP_MJ_SET_SECURITY
- 安全检查 WDK 文件系统，IRP_MJ_QUERY_SECURITY
- 安全描述符 WDK 文件系统，安全检查
- 描述符文件系统，安全检查
- 检索安全描述符
- 查询安全描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3af3974855b9cef7294549ef391e0c5c267b2897
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836449"
---
# <a name="irp_mj_query_security-and-irp_mj_set_security"></a>IRP \_ mj \_ 查询 \_ 安全性和 irp \_ mj \_ 设置 \_ 安全性


幸运的是，对于文件系统，安全描述符的实际存储和检索相对不透明。 这是由自相关格式的安全描述符的性质引起的，无需对文件系统进行任何理解。 因此，处理查询操作通常是一种非常简单的做法。 下面是文件系统实现的示例：

```cpp
NTSTATUS FsdCommonQuerySecurity( PIRP_CONTEXT IrpContext)
{
    NTSTATUS status = STATUS_SUCCESS;
    PSECURITY_DESCRIPTOR LocalPointer;

    // Need to add code to lock the FCB here

    status = FsdLoadSecurityDescriptor(IrpContext, IrpContext->Fcb);
 
    if (NT_SUCCESS(status) ) {
 
        //
        // copy the SecurityDescriptor into the callers buffer
        // note that this copy can throw an exception that must be handled
        // (code to handle the exception was omitted here for brevity)
        //
        LocalPointer = IrpContext->Fcb->SecurityDescriptor;

        status = SeQuerySecurityDescriptorInfo(
     &IrpContext->IrpSp->Parameters.QuerySecurity.SecurityInformation,
            (PSECURITY_DESCRIPTOR)IrpContext->Irp->UserBuffer,
            &IrpContext->IrpSp->Parameters.QuerySecurity.Length,
            &LocalPointer );
 
        //
        // CACLS utility expects OVERFLOW
        //
        if (status == STATUS_BUFFER_TOO_SMALL ) {
            status = STATUS_BUFFER_OVERFLOW;
        }
    }
 
    // Need to add code to unlock the FCB here

    return status;
}
```

请注意，此例程依赖于外部函数从此实现中的持久性存储 (加载实际安全描述符，因此，仅在以前未) 加载安全描述符的情况下才加载它。 因为安全描述符对文件系统不透明，所以必须使用安全引用监视器将描述符复制到用户的缓冲区中。 对于此代码示例，请注意两个要点：

1.  \_ \_ \_ \_ \_ 若要为某些 Windows 安全工具提供正确的行为，必须将错误代码状态缓冲区转换为警告代码状态缓冲区溢出。

2.  处理用户缓冲区时可能会发生错误，这是因为查询和设置的安全操作通常都是直接使用用户缓冲区来完成的。 请注意，这由文件系统创建的设备对象的 **Flags** 成员控制 \_ 。 在基于此代码的文件系统实现中，调用函数需要使用 \_ \_ try 块来防范无效的用户缓冲区。

在此示例中，文件系统如何从存储中加载安全描述符 (**FsdLoadSecurityDescriptor** 函数) 将完全取决于文件系统中安全描述符存储的实现。

存储安全描述符更多。 如果文件系统支持安全描述符共享，则文件系统可能需要确定安全描述符是否与现有的安全描述符相匹配。 对于不匹配的安全描述符，文件系统可能需要为此新的安全描述符分配新存储。 下面是一个用于替换文件上的安全描述符的示例例程。

```cpp
NTSTATUS FsdCommonSetSecurity(PIRP_CONTEXT IrpContext)
{
    NTSTATUS status = STATUS_SUCCESS;
    PSECURITY_DESCRIPTOR SavedDescriptorPtr = 
        IrpContext->Fcb->SecurityDescriptor;
    ULONG SavedDescriptorLength = 
        IrpContext->Fcb->SecurityDescriptorLength;
    PSECURITY_DESCRIPTOR newSD = NULL;
    POW_FCB Fcb = IrpContext->Fcb;
    ULONG Information = IrpContext->Irp->IoStatus.Information;

    //
    // make sure that the FCB security descriptor is up to date
    //
    status = FsdLoadSecurityDescriptor(IrpContext, Fcb);

    if (!NT_SUCCESS(status)) {
      //
      // Something is seriously wrong 
      //
      IrpContext->Irp->IoStatus.Status = status;
      IrpContext->Irp->IoStatus.Information = 0;
      return status;
    }        
 
    status = SeSetSecurityDescriptorInfo(
       NULL,
       &IrpContext->IrpSp->Parameters.SetSecurity.SecurityInformation,
       IrpContext->IrpSp->Parameters.SetSecurity.SecurityDescriptor,
       &Fcb->SecurityDescriptor,
       PagedPool,
       IoGetFileObjectGenericMapping()
       );

    if (!NT_SUCCESS(status)) {

        //
        // restore things  and return
        //
        Fcb->SecurityDescriptorLength = SavedDescriptorLength;
        Fcb->SecurityDescriptor = SavedDescriptorPtr;
        IrpContext->Irp->IoStatus.Status = status;
        IrpContext->Irp->IoStatus.Information = 0;

        return status;
    }

    //
    // get the new length
    //
    Fcb->SecurityDescriptorLength = 
        RtlLengthSecurityDescriptor(Fcb->SecurityDescriptor);

    //
    // allocate our own private SD to replace the one from
    // SeSetSecurityDescriptorInfo so we can track our memory usage
    //
    newSD = ExAllocatePoolWithTag(PagedPool, 
        Fcb->SecurityDescriptorLength, 'DSyM');

    if (!newSD) {
 
      //
      // paged pool is empty
      //
      SeDeassignSecurity(&Fcb->SecurityDescriptor);
      status = STATUS_NO_MEMORY;
      Fcb->SecurityDescriptorLength = SavedDescriptorLength;
      Fcb->SecurityDescriptor = SavedDescriptorPtr;
 
      //
      // make sure FCB security is in a valid state
      //
      IrpContext->Irp->IoStatus.Status = status;
      IrpContext->Irp->IoStatus.Information = 0;
 
      return status;
 
    } 
 
    //
    // store the new security on disk
    //
    status = FsdStoreSecurityDescriptor(IrpContext, Fcb);

    if (!NT_SUCCESS(status)) {
      //
      // great- modified the in-core SD but couldn't get it out
      // to disk. undo everything. 
      //
      ExFreePool(newSD);
      SeDeassignSecurity(&Fcb->SecurityDescriptor);
      status = STATUS_NO_MEMORY;
      Fcb->SecurityDescriptorLength = SavedDescriptorLength;
      Fcb->SecurityDescriptor = SavedDescriptorPtr;
      IrpContext->Irp->IoStatus.Status = status;
      IrpContext->Irp->IoStatus.Information = 0;
 
      return status;
    }
 
    //
    // if we get here everything worked! 
    //
    RtlCopyMemory(newSD, Fcb->SecurityDescriptor, 
        Fcb->SecurityDescriptorLength);
 
    //
    // deallocate the security descriptor
    //
    SeDeassignSecurity(&Fcb->SecurityDescriptor);
 
    //
    // this either is the new private SD or NULL if 
    // memory allocation failed
    //
    Fcb->SecurityDescriptor = newSD;

    //
    // free the memory from the previous descriptor
    //
    if (SavedDescriptorPtr) {
      //
      // this  must always be from private allocation
      //
      ExFreePool(SavedDescriptorPtr);
 
    }        
 
    IrpContext->Irp.IoStatus = status;
    IrpContext->Irp.Information = Information;

    return status;
}
```

请注意，这是一个实现方式明显不同于文件系统的区域。 例如，支持安全描述符共享的文件系统需要添加显式逻辑来查找匹配的安全描述符。 此示例仅尝试向实现者提供指导。

 

 





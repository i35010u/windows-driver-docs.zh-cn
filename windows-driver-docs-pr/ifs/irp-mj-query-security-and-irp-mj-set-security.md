---
title: IRP_MJ_QUERY_SECURITY 和 IRP_MJ_SET_SECURITY
description: IRP_MJ_QUERY_SECURITY 和 IRP_MJ_SET_SECURITY
ms.assetid: 64216496-55f0-4ad4-b475-341ed9eb6886
keywords:
- IRP_MJ_QUERY_SECURITY
- IRP_MJ_SET_SECURITY
- 安全 WDK 文件系统，添加安全检查
- 安全检查 WDK 的文件系统，IRP_MJ_SET_SECURITY
- 安全检查 WDK 的文件系统，IRP_MJ_QUERY_SECURITY
- 安全描述符 WDK 文件系统，安全检查
- 描述符 WDK 文件系统，安全检查
- 检索安全描述符
- 查询的安全描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7280f1d5c61f25f5088759481f5f48536f21b086
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520378"
---
# <a name="irpmjquerysecurity-and-irpmjsetsecurity"></a>IRP\_MJ\_查询\_安全性和 IRP\_MJ\_设置\_安全


幸运的是文件系统中，对于实际存储和检索的安全描述符操作是相对较不透明。 这是由于不需要了解任何描述符的文件系统的自相关格式的安全描述符的特性。 因此，处理查询操作通常是一个非常简单的练习。 下面是从文件系统实现示例：

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

请注意，此例程依赖于外部函数以加载实际的安全描述符从持久性存储区 （在此实现中，例程只能加载的安全描述符，如果它以前尚未加载）。 由于安全描述符是不透明的文件系统，则必须使用安全引用监视器将描述符复制到用户的缓冲区。 我们注意到两个点相对于此代码示例：

1.  错误代码状态的转换\_缓冲区\_过\_警告代码状态到小型\_缓冲区\_溢出才可为某些 Windows 安全工具提供正确的行为。

2.  因为两种查询，并且通常完成集合安全操作，会出现错误处理用户缓冲区可以和将，直接使用用户缓冲区。 请注意，这由控制**标志**设备的成员\_通过文件系统创建的对象。 在基于此代码的文件系统实现，调用的函数需要使用\_ \_try 块以防止无效用户缓冲区。

如何从存储加载文件系统的安全描述符的具体情况 ( **FsdLoadSecurityDescriptor**函数在此示例中) 将取决于完全实现的安全描述符存储在文件系统中。

存储安全描述符是稍微要复杂。 文件系统可能需要确定是否安全描述符共享文件系统支持的安全描述符是否匹配现有的安全描述符。 对于不匹配的安全描述符，文件系统可能需要为此新的安全描述符分配新的存储空间。 下面是用于替换上一个文件的安全描述符的示例例程。

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
        Fcb->SecurityDescriptorLength, &#39;DSyM&#39;);

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
      // great- modified the in-core SD but couldn&#39;t get it out
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

请注意，这是哪一种实现中的某个区域会发生显著变化从文件系统到文件系统。 例如，支持安全描述符共享的文件系统将需要添加显式逻辑来查找匹配的安全描述符。 此示例是仅尝试为实施者提供的指导。

 

 





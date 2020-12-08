---
title: 将安全性分配给 IRP_MJ_CREATE 上的新文件
description: 将安全性分配给 IRP_MJ_CREATE 上的新文件
keywords:
- IRP_MJ_CREATE
- 新文件安全性 WDK 文件系统
- 安全检查 WDK 文件系统，IRP_MJ_CREATE
- 安全描述符 WDK 文件系统，新文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 793d73239b073be34ddfb98bc96da6f7c3f68fd9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799569"
---
# <a name="assigning-security-to-a-new-file-on-irp_mj_create"></a>将安全性分配给 IRP \_ MJ CREATE 上的新文件 \_


## <span id="ddk_assigning_security_to_a_new_file_on_irp_mj_create_if"></span><span id="DDK_ASSIGNING_SECURITY_TO_A_NEW_FILE_ON_IRP_MJ_CREATE_IF"></span>


"创建处理" 中的最后一项任务是将安全性分配给新的文件。 虽然 Windows 安全模型支持继承 (单个 ACE 项标记为在创建新文件或目录时继承，而在文件系统外实现) 。 因此，文件系统中的大部分逻辑都专用于存储新的安全描述符。 下面是一个示例例程：

```cpp
NTSTATUS FsdAssignInitialSecurity( PIRP_CONTEXT IrpContext, 
        PFCB Fcb, PFCB Directory)
{
    NTSTATUS status = STATUS_SUCCESS;
    BOOLEAN CreateDir = ((IrpContext->IrpSp->Parameters.Create.Options
        & FILE_DIRECTORY_FILE)==FILE_DIRECTORY_FILE);
    PACCESS_STATE AccessState = 
    IrpContext->IrpSp->Parameters.Create.SecurityContext->AccessState;
    PSECURITY_DESCRIPTOR SecurityDescriptor = NULL;

    //
    // Make sure the parent directory's security descriptor is loaded.
    //
    (void) FsdLoadSecurityDescriptor(IrpContext, Directory);

    //
    // don't care about the return code here, as it is handled later
    //
    if (Directory->SecurityDescriptor == NULL) {

        //
        // If the parent has no security, then we are outside
        // of the normal Windows paradigm.
        //
        // The child (that is, the target of the create) will also have
        // a NULL SD.
        //
        // Note that you can always assign security to the file object 
        // explicitly at later on.
        //
        return STATUS_SUCCESS;

    }

    //
    // Now create the security descriptor.
    //
    status = SeAssignSecurity(Directory->SecurityDescriptor, 
                              AccessState->SecurityDescriptor,
                              &SecurityDescriptor, 
                              CreateDir, 
                              &AccessState->SubjectSecurityContext,
                              IoGetFileObjectGenericMapping(),
                              PagedPool);

    if (!NT_SUCCESS(status)) {

        return status;
    }

    //
    // Associate the SD with the file; use our own storage so when 
    // cleanup occurs it is unnecessary to know if the storage came from the 
    // security reference monitor.
     //
    Fcb->SecurityDescriptorLength = 
        RtlLengthSecurityDescriptor( SecurityDescriptor );
 
    Fcb->SecurityDescriptor = ExAllocatePoolWithTag(PagedPool, 
        Fcb->SecurityDescriptorLength, 'DSyM');

    if (!Fcb->SecurityDescriptor) {
        //
        // There is no paged pool.
        //
        SeDeassignSecurity(&SecurityDescriptor);
        Fcb->SecurityDescriptorLength = 0;
        return STATUS_NO_MEMORY;
    }

    RtlCopyMemory(Fcb->SecurityDescriptor, SecurityDescriptor, 
        Fcb->SecurityDescriptorLength);
 
    SeDeassignSecurity(&SecurityDescriptor);
 
    //
    // Store the SD persistently (this is file system specific).
    //
    (void) FsdStoreSecurityDescriptor(IrpContext, Fcb);

    return STATUS_SUCCESS;
}
```

请注意，构造初始安全描述符 (了解继承的逻辑，例如) 不在文件系统中进行处理。 这与在文件系统层中处理安全描述符的简单模型保持一致。

 

 





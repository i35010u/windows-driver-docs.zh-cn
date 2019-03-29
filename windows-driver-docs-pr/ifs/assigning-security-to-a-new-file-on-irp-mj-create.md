---
title: 将安全性分配给 IRP_MJ_CREATE 上的新文件
description: 将安全性分配给 IRP_MJ_CREATE 上的新文件
ms.assetid: f01a09c4-f71f-4b9e-99c8-9bc7ca5ca316
keywords:
- IRP_MJ_CREATE
- 新的文件安全 WDK 文件系统
- 安全检查 WDK 的文件系统，IRP_MJ_CREATE
- 安全描述符 WDK 文件系统，新的文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9d9b60374ee4c7f214f8bfc887b7e1c5f316c74
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350270"
---
# <a name="assigning-security-to-a-new-file-on-irpmjcreate"></a>将安全分配给新文件在 IRP\_MJ\_创建


## <span id="ddk_assigning_security_to_a_new_file_on_irp_mj_create_if"></span><span id="DDK_ASSIGNING_SECURITY_TO_A_NEW_FILE_ON_IRP_MJ_CREATE_IF"></span>


最后一个任务中的创建处理将安全性分配给新文件。 尽管 Windows 安全模型支持继承 (各 ACE 项标记的方式，它们继承时创建新文件或目录) 这实现的外部文件系统。 因此，在文件系统中的逻辑的大容量专用于存储的新的安全描述符。 下面是示例例程：

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

请注意不文件系统中处理构造 （例如了解继承） 的初始安全描述符的逻辑。 这是为了与用于处理安全描述符中的文件系统层在简单恢复模式保持一致。

 

 





---
title: IRP_MJ_SET_INFORMATION
description: IRP_MJ_SET_INFORMATION
ms.assetid: 2a6c837c-85c9-46d8-85d8-d779f22be54e
keywords:
- IRP_MJ_SET_INFORMATION
- 安全 WDK 文件系统，添加安全检查
- 安全检查 WDK 的文件系统，IRP_MJ_SET_INFORMATION
- 重命名操作 WDK 的文件系统
- 硬链接操作 WDK 文件系统
- 名称 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24f39466824de162db2b0b1e47447960bccaebe7
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349168"
---
# <a name="irpmjsetinformation"></a>IRP\_MJ\_SET\_INFORMATION


重命名和硬链接中设置信息的情况下可能需要在某些情况下安全检查。 具体而言，如果调用方想要通过设置，删除重命名或硬链接的目标**ReplaceIfExists**字段**TRUE**，文件系统必须执行安全检查，以确保调用方具有删除目标的适当权限。 此外，可以有某些类型的文件系统中，作为一种策略，不希望允许在这种方式中删除的文件 （注册表配置单元和分页文件，例如）。 下面的代码示例确定调用方是否具有要删除该文件的适当安全权限：

```cpp
NTSTATUS FsdCheckDeleteFileAccess(POW_IRP_CONTEXT IrpContext, 
                                  PSECURITY_DESCRIPTOR targetSD, 
                                  PFCB ParentFcb)
{
    SECURITY_SUBJECT_CONTEXT SubjectContext;
    BOOLEAN Granted;
    NTSTATUS status = STATUS_SUCCESS;
    PPRIVILEGE_SET Privileges = NULL;
    ACCESS_MASK GrantedAccess;

    //
    // See if the user has DELETE access to the target.
    //
    SeCaptureSubjectContext( &SubjectContext );

    SeLockSubjectContext( &SubjectContext );

    Granted = SeAccessCheck(targetSD,           // Target's SD.
                            &SubjectContext,    // Captured security context.
                            TRUE,               // Tokens are locked.
                            DELETE,             // we only care about delete 
                            0,                  // previously granted access.
                            &Privileges,        // privilege_set
                            IoGetFileObjectGenericMapping(), // Generic mappings.
                            UserMode,           // Mode
                            &GrantedAccess,     // Granted access mask
                            &status );          // Error code

    //
    // Do not need privilege set, so release it.
    //
    if (Privileges != NULL) { 

        SeFreePrivileges( Privileges ); 
        Privileges = NULL;
    }

    if (!Granted) {

        status = STATUS_SUCCESS;

        //
        // The user does not have DELETE access to the target, but 
        // could have FILE_DELETE_CHILD access to the parent directory.
        //
        (void) FsdLoadSecurityDescriptor(IrpContext, ParentFcb);
        if (!ParentFcb->SecurityDescriptor) {
            //
            // fine - no security is fine - he gets to do what he wants 
            //
            SeUnlockSubjectContext( &SubjectContext );
            SeReleaseSubjectContext( &SubjectContext );
            return STATUS_SUCCESS;
        }

 
        Granted = SeAccessCheck(&ParentFcb->SecurityDescriptor,
                                &SubjectContext,   // Captured security context.
                                TRUE,              // Tokens are locked.
                                FILE_DELETE_CHILD, // we only care about delete 
                                0,                 // Previously granted access.
                                &Privileges,       // privilege_set
                                IoGetFileObjectGenericMapping(), // Generic mappings
                                UserMode,          // mode
                                &GrantedAccess,    // Granted access mask
                                &status );         // Error code
        //
        // Release privileges
        //
        if (Privileges != NULL) { 
            SeFreePrivileges( Privileges ); 
            Privileges = NULL;
        }
    }
    SeUnlockSubjectContext( &SubjectContext );
    SeReleaseSubjectContext( &SubjectContext );
    return status;
}
```

此代码可用于重命名和硬链接创建用例。

请注意，它位于文件系统决定不允许删除要删除的文件的类型，本文档讨论策略级别代码的范围之外。

 

 





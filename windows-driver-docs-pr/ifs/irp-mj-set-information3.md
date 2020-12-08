---
title: IRP_MJ_SET_INFORMATION 上的安全检查
description: 描述文件系统对 IRP_MJ_SET_INFORMATION 进行安全检查的方式
keywords:
- IRP_MJ_SET_INFORMATION
- 安全 WDK 文件系统，添加安全检查
- 安全检查 WDK 文件系统，IRP_MJ_SET_INFORMATION
- 重命名操作 WDK 文件系统
- 硬链接操作 WDK 文件系统
- 命名 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da3c2796f3b04afc46b6463a09251aa95bacc39d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793755"
---
# <a name="security-checks-on-irp_mj_set_information"></a>IRP_MJ_SET_INFORMATION 上的安全检查

在某些情况下，"设置信息" 中的 "重命名" 和 "硬链接" 事例可能需要安全检查。 具体来说，如果调用方想要通过将 " **ReplaceIfExists** " 字段设置为 " **TRUE**" 来删除 "重命名" 或 "硬链接" 的目标，则文件系统必须执行安全检查，以确保调用方具有删除目标的适当权限。 此外，某些类型的文件系统（如策略）也可能不希望以这种方式删除 (注册表配置单元和页面文件，例如) 。 下面的代码示例确定调用方是否具有适当的安全权限来删除文件：

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
            // fine - no security is fine - the user gets to do what they want
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

此代码可用于重命名和硬链接创建案例。

请注意，它超出了本文档的范围，无法讨论文件系统根据要删除的文件类型决定禁止删除的策略级别代码。

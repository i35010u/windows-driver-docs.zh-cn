---
title: 在 IRP_MJ_CREATE 上添加审核
description: 在 IRP_MJ_CREATE 上添加审核
keywords:
- IRP_MJ_CREATE
- 审核 WDK 文件系统
- 安全检查 WDK 文件系统，IRP_MJ_CREATE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a583d43c114c6f5c56dc7e2a2b0d5f7bebef3872
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838473"
---
# <a name="adding-auditing-on-irp_mj_create"></a>在 IRP \_ MJ CREATE 上添加审核 \_


## <span id="ddk_adding_auditing_on_irp_mj_create_if"></span><span id="DDK_ADDING_AUDITING_ON_IRP_MJ_CREATE_IF"></span>


文件系统中安全检查的另一个重要方面是在必要时添加审核 () 。 通常，这是作为一组做出安全决策的例程的一部分来完成的，因为审核的目的是记录系统所做的安全决策。 例如，以下代码可用于在完成访问检查后在文件系统内实现审核：

```cpp
{
UNICODE_STRING FileAuditObjectName;

RtlInitUnicodeString(&FileAuditObjectName, L"File");

if ( SeAuditingFileOrGlobalEvents (AccessGranted, 
        &Fcb->SecurityDescriptor, 
        &AccessState->SubjectSecurityContext)) {
    //
    // Must pass complete Windows path name, including device name.
    //
    ConstructAuditFileName(Irp, Fcb, &AuditName);

    if (IrpSp->Parameters.Create.SecurityContext->FullCreateOptions 
            & FILE_DELETE_ON_CLOSE) {
        SeOpenObjectForDeleteAuditAlarm(&FileAuditObjectName,
                                        NULL,
                                        &AuditName,
                                        &Fcb->SecurityDescriptor,
                                        AccessState,
                                        FALSE, // Object not created.
                                        // Was it  successful?  
                                        // Based on SeAccessCheck
                                        SeAccessCheckAccessGranted, 
                                        // UserMode or KernelMode
                                        EffectiveMode, 
                                        &AccessState->GenerateOnClose
                                        );
    } else {
        SeOpenObjectAuditAlarm(&FileAuditObjectName,
                               NULL,
                               &AuditName,
                               &Fcb->SecurityDescriptor,
                               AccessState,
                               FALSE, // object not created
                               // Was it successful?  
                               // Based on SeAccessCheck
                               AccessGranted, 
                               // UserMode or KernelMode
                               EffectiveMode, 
                               &AccessState->GenerateOnClose
                               );
    }

    //
    // Free file name here if needed.
    //
}
```

 

 





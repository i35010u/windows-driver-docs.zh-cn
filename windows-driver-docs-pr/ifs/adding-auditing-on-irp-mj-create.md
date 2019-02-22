---
title: 添加对 IRP_MJ_CREATE 审核
description: 添加对 IRP_MJ_CREATE 审核
ms.assetid: cb71fe83-44f4-48dd-8fff-250f1d27c123
keywords:
- IRP_MJ_CREATE
- 审核 WDK 的文件系统
- 安全检查 WDK 的文件系统，IRP_MJ_CREATE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a96484269cbd7d72e31972fbc45fa950128f1cae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556198"
---
# <a name="adding-auditing-on-irpmjcreate"></a>添加审核 IRP\_MJ\_创建


## <span id="ddk_adding_auditing_on_irp_mj_create_if"></span><span id="DDK_ADDING_AUDITING_ON_IRP_MJ_CREATE_IF"></span>


文件系统中的安全检查的另一个重要方面是添加审核 （如有必要）。 通常情况下，这是同一组做出安全决策，因为审核的目的是为了记录所做的系统的安全决策的例程的一部分。 例如，下面的代码可以用于实现审核文件系统中完成访问检查后：

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

 

 





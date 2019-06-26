---
title: 检查 IRP_MJ_CREATE 上的遍历特权
description: 检查 IRP_MJ_CREATE 上的遍历特权
ms.assetid: 9ba743d6-8e78-4f9a-9cb8-cb98f734c290
keywords:
- IRP_MJ_CREATE
- 遍历 WDK 的文件系统权限
- 安全检查 WDK 的文件系统，IRP_MJ_CREATE
- WDK 的文件系统权限
- WDK 的文件系统路径
- 通用安全检查 WDK 的文件系统
- SeChangeNotifyPrivilege
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a059177cf75eb3c1236b954ae12f6efc3bed262
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379001"
---
# <a name="checking-for-traverse-privilege-on-irpmjcreate"></a>检查遍历特权 IRP\_MJ\_创建


## <span id="ddk_checking_for_traverse_privilege_on_irp_mj_create_if"></span><span id="DDK_CHECKING_FOR_TRAVERSE_PRIVILEGE_ON_IRP_MJ_CREATE_IF"></span>


主要关心的问题之一[ **IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)检查是，调用方是否有遍历权限 （调用方没有访问该对象的路径的权限）。 由于大多数调用方有遍历权限，通常在文件系统中完成的第一个检查之一检查遍历权限：

```cpp
    BOOLEAN traverseCheck = 
        !(IrpContext->IrpSp->Parameters.Create.SecurityContext->AccessState->Flags
            & TOKEN_HAS_TRAVERSE_PRIVILEGE);
```

请注意，遍历特权检查依赖于从 I/O 管理器传递到文件系统的状态信息。 此信息取决于调用方是否持有 SeChangeNotifyPrivilege。 如果调用方不持有此特权，必须在每个目录上完成的遍历检查。 在下面的遍历检查的示例是使用通用例程完成，通常用于大多数安全检查：

{

```cpp
    SeLockSubjectContext(
        &accessParams.AccessState->SubjectSecurityContext);
//
// Note: AccessParams is passed to us and is normally based on
//       the fields of the same name from the IRP
//

    granted = SeAccessCheck( Fcb->SecurityDescriptor,
        &AccessParams.AccessState->SubjectSecurityContext,
        TRUE,
        AccessParams.desiredAccess,
        0,
        &Privileges,
        IoGetFileObjectGenericMapping(),
        AccessParams.AccessMode,
        &AccessParams.GrantedAccess,
        &AccessParams.status );

    if (Privileges != NULL) {
        //
        // this changes the AccessState
        //
        (void) SeAppendPrivileges(AccessParams.AccessState, Privileges );
        SeFreePrivileges( Privileges );
        Privileges = NULL;
    }

    if (granted) {
        //
        // delete granted bits from desired bits
        //
        AccessParams.desiredAccess &= 
            ~(AccessParams.GrantedAccess | MAXIMUM_ALLOWED);
 
        if (!checkOnly) {
        //
        // the caller wants to modify the access state for this 
        // request
        //
            AccessParams.AccessState->PreviouslyGrantedAccess |= 
                AccessParams.GrantedAccess;

        if (maxDesired) {

            maxDelete = 
                (BOOLEAN)(AccessParams.AccessState->PreviouslyGrantedAccess & 
                    DELETE);
            maxReadAttr = 
                (BOOLEAN)(AccessParams.AccessState->PreviouslyGrantedAccess & 
                    FILE_READ_ATTRIBUTES);
        }
        AccessParams.AccessState->RemainingDesiredAccess &= 
            ~(AaccessParams.GrantedAccess | MAXIMUM_ALLOWED);
    }
    SeUnlockSubjectContext(&accessParams.AccessState->SubjectSecurityContext);  
}
```

此函数执行的常规安全检查。 此函数必须应对在此过程中的以下问题：

-   它必须指定要用于检查正确的安全描述符。

-   应用程序必须通过沿 （这些是执行该操作的实体的凭据） 的安全上下文。

-   它必须更新基于安全检查的结果的访问状态。

-   它必须考虑到了最大值\_允许选项 （请参阅 ntifs.h 包括 WDK 包含详细信息的文件）。 最大值\_允许选项指定的文件系统应设置为文件系统允许的最大可能访问权限的访问权限 （读取/写入/删除，例如）。 应用程序很少使用的最大\_允许选项，因为 FASTFAT 文件系统上不支持此选项。 因为最大值\_允许选项位不是一个 FASTFAT 文件系统可以识别访问位，它会拒绝对给定文件的访问请求。 尝试使用最大打开 FASTFAT 卷上的文件的应用程序\_允许选项集找到的请求会失败。 有关详细信息，请参阅**FatCheckFileAccess** Acchksup.c 源文件的 WDK 包含 FASTFAT 示例代码中的函数。

请注意，进行简单遍历检查，请求的访问将是文件\_遍历和安全描述符将该目录的调用方尝试遍历时，不从原始 IRP所请求的访问通过\_MJ\_创建 IRP。

 

 





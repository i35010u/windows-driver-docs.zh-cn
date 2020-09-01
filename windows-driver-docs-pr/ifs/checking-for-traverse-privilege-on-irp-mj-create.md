---
title: 检查 IRP_MJ_CREATE 上的遍历特权
description: 检查 IRP_MJ_CREATE 上的遍历特权
ms.assetid: 9ba743d6-8e78-4f9a-9cb8-cb98f734c290
keywords:
- IRP_MJ_CREATE
- 遍历特权 WDK 文件系统
- 安全检查 WDK 文件系统，IRP_MJ_CREATE
- 权限 WDK 文件系统
- 路径 WDK 文件系统
- 一般安全检查 WDK 文件系统
- SeChangeNotifyPrivilege
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 749715617d9f2a75ed04f72e6c095ed8873f8304
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065344"
---
# <a name="checking-for-traverse-privilege-on-irp_mj_create"></a>检查 IRP \_ MJ CREATE 的遍历特权 \_


## <span id="ddk_checking_for_traverse_privilege_on_irp_mj_create_if"></span><span id="DDK_CHECKING_FOR_TRAVERSE_PRIVILEGE_ON_IRP_MJ_CREATE_IF"></span>


[**IRP \_ MJ \_ 创建**](./irp-mj-create.md)检查的主要问题之一是调用方是否具有遍历特权 (调用方是否有权访问对象) 的路径。 由于大多数调用方具有遍历权限，因此在文件系统中执行的第一个检查通常是检查遍历特权：

```cpp
    BOOLEAN traverseCheck = 
        !(IrpContext->IrpSp->Parameters.Create.SecurityContext->AccessState->Flags
            & TOKEN_HAS_TRAVERSE_PRIVILEGE);
```

请注意，遍历特权检查依赖于从 i/o 管理器传递到文件系统的状态信息。 此信息取决于调用方是否包含 SeChangeNotifyPrivilege。 如果调用方不具有此权限，则必须对每个目录执行遍历检查。 在下面的示例中，遍历检查使用一般例程完成，通常用于大多数安全检查：

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

此函数执行常规安全检查。 此函数必须处理以下问题：

-   它必须指定要用于检查的正确的安全描述符。

-   它必须通过安全上下文传递 (这些是执行) 操作的实体的凭据。

-   它必须根据安全检查的结果更新访问状态。

-   它必须考虑到 "允许的最大值" \_ 选项 (有关详细信息) ，请参阅 WDK 包含的 ntifs 包含文件。 "允许的最大值" \_ 选项指定文件系统应将访问权限设置为文件系统 (读取/写入/删除允许的最大可能访问权限，例如) 。 很少有应用程序使用 "最大 \_ 允许" 选项，因为 FASTFAT 文件系统不支持此选项。 由于允许的最大 \_ 选项位不是 FASTFAT 文件系统识别的访问位之一，因此它将拒绝对给定文件的访问请求。 尝试使用 "允许的最大值" 选项集在 FASTFAT 卷上打开文件的应用程序 \_ 将发现请求失败。 有关详细信息，请参阅 WDK 包含的 FASTFAT 示例代码的 Acchksup 源文件中的 **FatCheckFileAccess** 函数。

请注意，对于简单遍历检查，请求的访问将是文件 \_ 遍历，而安全描述符应是调用方尝试遍历的目录的安全描述符，而不是从原始 IRP \_ MJ CREATE IRP 请求的访问权限 \_ 。

 


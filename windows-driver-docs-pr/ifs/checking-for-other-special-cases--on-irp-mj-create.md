---
title: 检查 IRP_MJ_CREATE 上的其他特殊情况
description: 检查 IRP_MJ_CREATE 上的其他特殊情况
keywords:
- IRP_MJ_CREATE
- 安全检查 WDK 文件系统，IRP_MJ_CREATE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d1c45fec0db82ad16ee9d4baaf2a778189b7703
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818457"
---
# <a name="checking-for-other-special-cases-on-irp_mj_create"></a>检查 IRP \_ MJ CREATE 上的其他特殊 \_ 情况


## <span id="ddk_checking_for_other_special_cases_on_irp_mj_create_if"></span><span id="DDK_CHECKING_FOR_OTHER_SPECIAL_CASES_ON_IRP_MJ_CREATE_IF"></span>


如果调用方没有 SeChangeNotifyPrivilege，则在 IRP MJ 中创建处理时，必须在 \_ 文件系统内进行其他特殊情况处理 \_ 。 例如，可以使用其文件 ID 或对象 ID 打开的文件可能不允许调用方获取该文件的路径，因为调用方可能没有通过目录树结构访问对象的遍历权限。

你可能希望在文件系统中考虑以下情况：

-   **文件 \_\_按 \_ 文件 \_ ID 打开**-不应将该文件的名称提供给调用方。 由于此信息 (遍历权限) 仅在创建操作过程中是已知的，并且在文件信息查询调用过程中将不可用，因此，在 IRP MJ 创建过程中，必须由文件系统来计算遍历权限的信息 \_ \_ 。

-   **SL \_打开 \_ 目标 \_ 目录** -目标文件可能不存在，必须检查目录以进行文件创建访问。 如果目标存在，则可能需要删除访问权限检查。 通常，在执行重命名操作时，会在 IRP \_ MJ \_ 设置信息处理过程中执行删除访问检查 \_ 。

-   **文件 \_替代** 和 **文件 \_ 覆盖** -破坏性操作需要额外的访问权限，即使调用方未显式请求它们。 例如，文件系统可能需要 "删除" 访问权限才能执行替代操作。

-   **文件 \_创建**， **打开文件， \_ \_ 如果** 和 **文件 \_ 覆盖， \_ 则** 为：建设性操作需要访问在其中创建新对象的父目录。 这是对包含目录的检查，而不是对象本身，因此类似于早期的代码示例。

-   **SL \_强制 \_ 访问 \_ 检查** -如果在 i/o 堆栈位置中设置此值，则必须执行检查，就好像调用是从用户模式而不是内核模式一样。 因此，即使调用源自内核模式服务器，对安全监视器例程的调用也应该指定 **UserMode** 。

-   *文件/目录删除* -这可能基于文件的 ACL 状态 (例如，文件 \_ 写入 \_ 数据访问隐式允许删除; 如果可以删除数据，则对该文件具有有效的 "删除" 权限，) 以及该目录的 ACL 状态 ("对包含目录的 ' 文件 \_ 删除 \_ 子权限"，例如) 。

下面的代码示例演示了文件替代和文件覆盖的特殊用例处理 \_ \_ ，这两种情况下，调用方隐式需要其他访问，即使未请求。

```cpp
{
ULONG NewAccess = Supersede ? DELETE : FILE_WRITE_DATA;
ACCESS_MASK AddedAccess = 0;
PACCESS_MASK DesiredAccess = 
    &IrpSp->Paramters.Create.SecurityContext->DesiredAccess;

//
// If the caller does not have restore privilege, they must have write
// access to the EA and attributes for overwrite or supersede.
//
if (0 == (AccessState->Flags & TOKEN_HAS_RESTORE_PRIVILEGE)) {
    *DesiredAccess |= FILE_WRITE_EA | FILE_WRITE_ATTRIBUTES;

    //
    // Does the caller already have this access?
    //
    if (AccessState->PreviouslyGrantedAccess & NewAccess) {

        //
        // No - they need this as well
        //
        *DesiredAccess |= NewAccess;

    }

    //
    // Now check access using SeAccessCheck (omitted)
    //

}
```

此代码示例是一个很好的示例，其中的文件系统策略优先。 调用方不请求删除访问或文件 \_ 写入 \_ 数据访问，但此类访问在基于文件系统的语义执行的操作中是固有的。

 

 





---
title: 对于上 IRP_MJ_CREATE 其他特殊情况检查
description: 对于上 IRP_MJ_CREATE 其他特殊情况检查
ms.assetid: e6af44c2-fd39-469b-8530-cf88edb329f7
keywords:
- IRP_MJ_CREATE
- 安全检查 WDK 的文件系统，IRP_MJ_CREATE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ae199707dd666930830389a644e4f366124bcc5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386331"
---
# <a name="checking-for-other-special-cases-on-irpmjcreate"></a>检查其他特殊情况下在 IRP\_MJ\_创建


## <span id="ddk_checking_for_other_special_cases_on_irp_mj_create_if"></span><span id="DDK_CHECKING_FOR_OTHER_SPECIAL_CASES_ON_IRP_MJ_CREATE_IF"></span>


其他特殊案例处理必须出现在 IRP\_MJ\_处理文件系统中，如果调用方不具有 SeChangeNotifyPrivilege 的创建。 例如，可以通过使用其文件 ID 或对象 ID 打开的文件可能不允许调用方以获取该文件的路径，因为调用方可能无权遍历目录树结构通过处理该对象的权限。

你可能想在文件系统中要考虑的情况下：

-   **文件\_开放\_BY\_文件\_ID** — 文件的名称不应将提供给调用方。 由于此信息 （遍历权限） 在创建操作时，仅知道和文件信息查询调用期间将不可用，因此必须在 IRP 期间通过文件系统计算遍历权限的信息\_MJ\_创建。

-   **SL\_开放\_目标\_DIRECTORY** — 可能不存在目标文件和目录必须检查的文件创建访问权限。 如果目标存在，则可能需要删除访问权限检查。 删除访问检查期间 IRP 重命名操作时的完成通常\_MJ\_设置\_信息处理。

-   **文件\_SUPERSEDE**并**文件\_覆盖** — 破坏性操作要求的其他访问权限，即使调用方没有显式请求它们。 例如，文件系统可能需要删除访问权限才能执行 supersede 操作。

-   **文件\_创建**，**文件\_打开\_如果**，以及**文件\_覆盖\_如果** — 建设性操作要求对正在其上创建新的对象的父目录的访问。 此规则检查上包含目录而不是上对象本身，因此类似于上面的代码示例。

-   **SL\_FORCE\_访问权限\_检查** — 像调用是从用户模式下，不是内核模式一样，如果 I/O 堆栈位置中设置此值，必须执行检查。 因此，对安全监视例程的调用应指定**UserMode**即使在内核模式服务器发起的调用。

-   *文件/目录删除* -这可能会根据文件的 ACL 状态 (例如，文件\_编写\_数据访问隐式允许删除; 如果可以删除数据，您可以有效删除此文件的权限） 以及目录的 ACL 状态 (文件\_删除\_孩子的示例中的包含目录的权限)。

下面的代码示例演示如何处理文件的特殊情况下\_SUPERSEDE 和文件\_覆盖、 额外的访问权限隐式需要由调用方，即使未请求这两种情况。

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

此代码示例是一个不错的文件系统策略优先示例。 删除访问权限或文件，调用方没有请求\_编写\_数据访问，但这样的访问权限是固有的正在执行基于文件系统的语义的操作。

 

 





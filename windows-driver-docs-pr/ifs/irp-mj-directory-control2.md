---
title: IRP_MJ_DIRECTORY_CONTROL 上的安全检查
description: 描述文件系统对 IRP_MJ_DIRECTORY_CONTROL 进行安全检查的方式
keywords:
- IRP_MJ_DIRECTORY_CONTROL
- 安全 WDK 文件系统，添加安全检查
- 安全检查 WDK 文件系统，IRP_MJ_DIRECTORY_CONTROL
- 目录控制 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0ad55c8732fd21fbf9abbe8dfd37f9b37456829
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792255"
---
# <a name="security-checks-on-irp_mj_directory_control"></a>IRP_MJ_DIRECTORY_CONTROL 上的安全检查

在处理某些目录控制操作（特别是那些处理更改通知的操作）时，需要考虑安全性。 安全问题是目录更改通知可能返回有关已更改的特定文件的信息。 如果用户没有遍历目录路径的权限，则无法向用户返回有关更改的信息。 否则，用户现在可以使用一种机制来了解有关用户不应具有的目录的其他信息。

通过文件系统运行库支持目录更改通知，文件系统允许文件系统指定一个回调函数，以便在返回目录更改通知之前执行遍历检查。 此回调函数使用大量参数。 出于安全考虑，以下三个参数非常重要：

- *NotifyContext* 是更改通知处于活动状态的目录的上下文。 这将是传递给对 [**FsRtlNotifyFullChangeDirectory**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullchangedirectory)的调用的 *FsContext* 参数。

- *TargetContext* 是已更改的文件的上下文。 这将是文件系统在调用 [**fsrtlnotifyfilterreportchange 并且**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfilterreportchange)时传递的 *TargetContext* 参数。

- *SubjectContext* 是请求目录更改通知的线程的安全上下文。 这是文件系统在对 **FsRtlNotifyFullChangeDirectory** 进行目录更改通知调用时捕获的主题安全上下文。

发生更改时，文件系统会向文件系统运行时库指出这一点。 文件系统运行时库将调用文件系统提供的回调函数，以验证是否可以向调用方提供有关更改的信息。 请注意，如果调用方需要检查，则文件系统只需注册回调函数。 如果调用方未启用 SeChangeNotifyPrivilege （如调用方的安全令牌中的 TOKEN_HAS_TRAVERSE_PRIVILEGE 所示），则会出现这种情况。

在回调函数内，文件系统必须执行从 *NotifyContext* 参数指定的目录到由 *TargetContext* 参数指定的已更改文件的遍历检查。 下面的示例例程执行此类检查。

```cpp
BOOLEAN
FsdNotifyTraverseCheck (
    IN PDIRECTORY_CONTEXT OriginalDirectoryContext,
    IN PFILE_CONTEXT ModifiedDirectoryContext,
    IN PSECURITY_SUBJECT_CONTEXT SubjectContext
    )
{
  BOOLEAN AccessGranted = TRUE;
  PFILE_CONTEXT CurrentDirectoryContext;
  ACCESS_MASK GrantedAccess;
  NTSTATUS Status;
  PPRIVILEGE_SET Privileges = NULL;
  PFILE_CONTEXT TopDirectory;

  //
  //  Nothing to do if there is no file context.
  //
  if (ModifiedDirectoryContext == NULL) {

    return TRUE;
  }

  //
  // If the directory that changed is the original directory,
  // we can return , since the caller has access.
  // Note that the directory  context is unique to the specific
  // open instance, while the modified directory context
  // represents the per-file/directory context.
  // How these data structures work in your file system will vary.
  //
  if (OriginalDirectoryContext->FileContext == ModifiedDirectoryContext) {
    return TRUE;
  }

  //
  // Lock the subject context.
  //
  SeLockSubjectContext(SubjectContext);

  for( TopDirectory = OriginalDirectoryContext->FileContext,
          CurrentDirectoryContext = ModifiedDirectoryContext;
          CurrentDirectoryContext == TopDirectory || !AccessGranted;
          CurrentDirectoryContext = CurrentDirectoryContext->ParentDirectory) {
    //
    // Ensure we have the current security descriptor loaded for
    // this directory.
    //
    FsdLoadSecurity( NULL, CurrentDirectoryContext);

    //
    // Perform traverse check.
    //
    AccessGranted = SeAccessCheck(
            CurrentDirectoryContext->SecurityDescriptor,
            SubjectContext,
            TRUE,
            FILE_TRAVERSE,
            0,
            &Privileges,
            IoGetFileObjectGenericMapping(),
            UserMode,
            &GrantedAccess,
            &Status);

    //
    // At this point, exit the loop if access was not granted,
    // or if the parent directory is the same as where the change
    // notification was made.
    //

  }

  //
  // Unlock subject context.
  //
  SeUnlockSubjectContext(SubjectContext);

  return AccessGranted;
}
```

对于缓存安全信息或具有不同的数据结构以跟踪文件和目录的文件系统，此例程可能会有很大的差别 (例如，使用结构跟踪文件和目录之间的链接的文件) 。 在此示例中，不会考虑支持链接的文件系统，因为尝试简化示例。

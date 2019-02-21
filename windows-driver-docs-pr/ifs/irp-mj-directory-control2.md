---
title: IRP_MJ_DIRECTORY_CONTROL
description: IRP_MJ_DIRECTORY_CONTROL
ms.assetid: 27c2de1c-5550-4211-97cc-4c66f18d3b99
keywords:
- IRP_MJ_DIRECTORY_CONTROL
- 安全 WDK 文件系统，添加安全检查
- 安全检查 WDK 的文件系统，IRP_MJ_DIRECTORY_CONTROL
- 目录控制 WDK 的文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1455a0d7b5d65c1deeb0cd1931ead06facf9fec7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545134"
---
# <a name="irpmjdirectorycontrol"></a>IRP\_MJ\_DIRECTORY\_控件


安全性是一个考虑因素时处理某些目录控制操作，值得注意的是那些要处理更改通知。 安全关注点是目录更改通知可能会返回有关已更改的特定文件的信息。 如果用户不具有遍历到目录的路径的权限，无法向用户返回有关更改的信息。 否则，该用户现在拥有一种机制，帮助您了解有关用户不应具有的目录的其他信息。

支持通过文件系统运行时库的目录更改通知实现文件系统，以指定用于返回目录更改通知前执行的遍历检查的回调函数。 此回调函数包含大量参数。 为了安全起见，以下三个参数非常重要：

-   *NotifyContext*-更改通知是 active directory 的上下文。 这将是*FsContext*参数中传递给在调用**FsRtlNotifyFilterChangeDirectory**。 请注意， **FsRtlNotifyFilterChangeDirectory**适用于 Windows XP 及更高版本。 使用 Windows 2000 系统**FsRtlNotifyFullChangeDirectory**函数，这是类似。

-   *TargetContext*-已更改的文件的上下文。 这将是*TargetContext*调用时，通过文件系统传递参数**出现**。

-   *SubjectContext*-请求目录的线程的安全上下文更改通知。 这是对目录更改通知调用次捕获的文件系统的使用者安全上下文**FsRtlNotifyFilterChangeDirectory**。

当发生了更改时，文件系统将指示此到文件系统运行时库。 然后，文件系统运行时库将调用回调函数提供的文件系统来验证调用方可以提供有关更改的信息。 请注意，文件系统仅需要注册一个回调函数，如果该检查不需要调用方。 这是这种情况，如果调用方不具有 SeChangeNotifyPrivilege 启用，如标记所示\_HAS\_遍历\_调用方的安全令牌中的特权。

在回调函数中，文件系统必须从指定的目录执行遍历检查*NotifyContext*参数，发生更改时，由指定的文件*TargetContext*参数。 下面的示例例程执行此类检查。

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
  //  Nothing to do  if there is no file context.
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

此例程很可能差别很大的缓存安全信息的文件系统或具有不同的数据结构，用于跟踪文件和目录 (例如，用于跟踪文件之间的链接使用结构的文件和目录）。 支持链接的文件系统不会考虑在此示例中，以尝试简化的示例。

 

 





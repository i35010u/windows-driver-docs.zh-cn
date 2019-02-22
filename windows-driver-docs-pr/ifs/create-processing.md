---
title: 创建处理
description: 创建处理
ms.assetid: c15a56d2-47db-4124-8250-f25f69d2d4e3
keywords:
- 安全 WDK 文件系统，语义模型检查
- 语义模型检查 WDK 的文件系统中，创建处理
- 创建处理 WDK 文件系统
- 安全引用监视器 WDK
- IRP_MJ_CREATE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79f5ed7a4bbf9de3ef852e25487b7bb6725ba2e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546389"
---
# <a name="create-processing"></a>创建处理


## <span id="ddk_create_processing_if"></span><span id="DDK_CREATE_PROCESSING_IF"></span>


文件系统，过程中发生的有趣的安全工作的大部分[ **IRP\_MJ\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff548630)处理。 它是此步骤，必须分析传入的请求，确定调用方是否具有适当的权限来执行此操作，并授予或拒绝相应操作。 幸运的是，对于文件系统开发人员，大部分决策机制是在中实现安全引用监视器。 因此，在大多数情况下，文件系统仅需要调用适当的安全引用监视器例程，以正确确定的访问权限。 文件系统的风险发生时调用这些例程根据需要将失败并不恰当地向调用方授予访问权限。

对于标准文件系统，如 FAT 文件系统中，作为 IRP 的一部分进行检查\_MJ\_创建一些主要语义检查。 例如，FAT 文件系统具有大量检查，以确保该 IRP\_MJ\_创建处理允许基于文件或目录的状态。 FAT 文件系统进行这些检查包括检查只读媒体 （例如，尝试执行破坏性"创建"操作，因此覆盖或取代，在只读介质上不允许），共享访问权限检查和 oplock 检查。 此分析的最困难的部分之一是要意识到在某一级别 （例如文件级别） 的操作实际上可能会禁止由于不同的级别资源的状态 （例如在卷级别）。 例如，如果另一个进程以独占方式锁定了该卷可能未打开的文件。 常见用例以检查包括：

-   是在文件级别打开符合卷级状态？ 必须遵守卷级锁定。 因此，如果一个进程持有一个独占的卷级锁，则该进程内的唯一线程可以打开文件。 从其他进程的线程必须不能打开文件。

-   是的文件打开媒体状态与兼容级别？ 某些"创建"操作修改的文件"创建"操作的一部分。 这将包括覆盖，取代，并甚至更新的上次访问的时间的文件。 这些"创建"操作不允许在只读介质上，不更新上次访问时间。

-   是的卷级别打开文件级别状态与兼容？ 如果已存在的卷上打开的文件，将不允许独占的卷打开。 这是新的开发人员经常遇到的问题，因为它们尝试打开该卷，并找到，它将失败。 当此操作失败，FSCTL\_卸除\_卷可用于使打开的句柄无效，并强制卸除，从而允许到新装载的卷的独占访问权限。

此外，文件属性必须兼容。 只读属性的文件无法打开以进行写访问。 请注意在展开的泛型权利扩展后，应检查所需的访问权限。 例如，此检查 FASTFAT 文件系统中的处于**FatCheckFileAccess**函数 （请参阅 Acchksup.c 源文件从 WDK 包含 fastfat 示例）。

下面的代码示例是特定于 FAT 语义。 实现 Dacl 的文件系统会执行额外的安全检查使用的安全引用监视器例程 ([**SeAccessCheck**](https://msdn.microsoft.com/library/windows/hardware/ff563674)，例如。)

```cpp
    //
    //  check for a read-only Dirent
    //

    if (FlagOn(DirentAttributes, FAT_DIRENT_ATTR_READ_ONLY)) {

        //
        //  Check the desired access for a read-only Dirent
        // Don&#39;t allow 
        //  WRITE, FILE_APPEND_DATA, FILE_ADD_FILE,
        //  FILE_ADD_SUBDIRECTORY, and FILE_DELETE_CHILD
        //

        if (FlagOn(*DesiredAccess, ~(DELETE |
                                     READ_CONTROL |
                                     WRITE_OWNER |
                                     WRITE_DAC |
                                     SYNCHRONIZE |
                                     ACCESS_SYSTEM_SECURITY |
                                     FILE_READ_DATA |
                                     FILE_READ_EA |
                                     FILE_WRITE_EA |
                                     FILE_READ_ATTRIBUTES |
                                     FILE_WRITE_ATTRIBUTES |
                                     FILE_EXECUTE |
                                     FILE_LIST_DIRECTORY |
                                     FILE_TRAVERSE))) {

            DebugTrace(0, Dbg, "Cannot open readonly\n", 0);

            try_return( Result = FALSE );
        }
```

由 FASTFAT 实现的更微妙检查是为了确保由调用方请求的访问权限是一些有关哪些 FAT 文件系统是注意 (在**FatCheckFileAccess**从 fastfat 中 Acchksup.c 函数示例 WDK包含）：

下面的代码示例演示了文件系统安全的一个重要概念。 检查以确保内容传递到文件系统不在预期的界限外。 中角度来看，保守估计，正确方法是安全的，如果您不了解访问请求，应拒绝该请求。

```cpp
    //
    // Check the desired access for the object. 
    // Reject what we do not understand.
    // The model of file systems using ACLs is that
    // they do not type the ACL to the object that the 
    // ACL is on. 
    // Permissions are not checked for consistency vs.
    // the object type - dir/file.
    //

    if (FlagOn(*DesiredAccess, ~(DELETE |
                                 READ_CONTROL |
                                 WRITE_OWNER |
                                 WRITE_DAC |
                                 SYNCHRONIZE |
                                 ACCESS_SYSTEM_SECURITY |
                                 FILE_WRITE_DATA |
                                 FILE_READ_EA |
                                 FILE_WRITE_EA |
                                 FILE_READ_ATTRIBUTES |
                                 FILE_WRITE_ATTRIBUTES |
                                 FILE_LIST_DIRECTORY |
                                 FILE_TRAVERSE |
                                 FILE_DELETE_CHILD |
                                 FILE_APPEND_DATA))) {

        DebugTrace(0, Dbg, "Cannot open object\n", 0);

        try_return( Result = FALSE );
    }
```

幸运的是文件系统后安全检查已完成在初始创建 I/O 管理器执行检查的处理，后续的安全。 因此，例如，I/O 管理器可确保用户模式应用程序仅用于读访问情况下不执行针对已打开的文件的写入操作。 实际上，文件系统不应尝试强制执行对文件对象的只读语义即使在仅进行读取访问，它已打开期间 IRP\_MJ\_写入调度例程。 这是由于内存管理器将与给定的部分对象相关联的特定文件对象的方法。 通过该部分的后续写入会作为 IRP 发送\_MJ\_编写文件对象上的操作，即使该文件以只读方式打开。 文件句柄转换为在 Nt 系统服务入口点通过相应的文件对象时，换而言之，完成访问强制执行[ **ObReferenceObjectByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff558679)。

有两个其他位置中的文件系统语义安全检查必须进行"创建"处理类似于：

-   在重命名或硬链接处理。

-   当处理文件系统控制操作。

后续各部分讨论了重命名处理和文件系统控制处理。

请注意，这不是语义问题相关的"创建"处理的详尽列表。 本部分的目的是为文件系统开发人员吸引人们关注这些问题。 必须为特定的文件系统标识、 实现以满足特定的语义和测试，以确保实现处理各种情况下所有语义问题。

 

 





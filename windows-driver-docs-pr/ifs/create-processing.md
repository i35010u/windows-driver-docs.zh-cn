---
title: 创建处理
description: 创建处理
ms.assetid: c15a56d2-47db-4124-8250-f25f69d2d4e3
keywords:
- 安全 WDK 文件系统，语义模型检查
- 语义模型检查 WDK 文件系统，创建处理
- 创建处理 WDK 文件系统
- 安全参考监视器 WDK
- IRP_MJ_CREATE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b05170d556d47091a0d9d06986d16572ebf4f570
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841453"
---
# <a name="create-processing"></a>创建处理


## <span id="ddk_create_processing_if"></span><span id="DDK_CREATE_PROCESSING_IF"></span>


对于文件系统，在[**IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)处理过程中，将会出现很多有趣的安全工作。 此步骤必须分析传入的请求，确定调用方是否有适当的权限来执行操作，并根据需要授予或拒绝操作。 幸运的是，对于文件系统开发人员而言，大部分决策机制都是在安全参考监视器内实现的。 因此，在大多数情况下，文件系统只需调用合适的安全引用监视器例程即可正确确定访问权限。 文件系统的风险在必要时无法调用这些例程，并且不恰当地授予调用方的访问权限。

对于标准文件系统，如 FAT 文件系统，作为 IRP\_MJ\_创建的一部分进行的检查主要是语义检查。 例如，FAT 文件系统具有多个检查，以确保基于文件或目录的状态允许 IRP\_MJ\_创建处理。 FAT 文件系统进行的这些检查包括对只读媒体的检查（例如，不允许对只读媒体执行破坏性的 "创建" 操作，如覆盖或取代、不允许在只读媒体上执行 "覆盖" 或 "取代"）、"共享访问检查" 和 "oplock 检查"。 此分析最难的部分之一就是在一个级别（例如，文件级别）上执行操作，因为有不同级别资源（例如，卷级别）的状态。 例如，如果另一个进程以独占方式锁定了该卷，则可能无法打开该文件。 常见的检查案例包括：

-   文件级别是否与卷级别状态兼容？ 卷级锁定必须为服从。 因此，如果一个进程持有一个独占量级锁，则只有该进程中的线程可以打开文件。 不得允许来自其他进程的线程打开文件。

-   文件级别是否与媒体状态兼容？ 某些 "创建" 操作会在 "创建" 操作过程中修改文件。 这包括覆盖、取代，甚至更新文件的上次访问时间。 不允许对只读媒体执行这些 "创建" 操作，并且不会更新上次访问时间。

-   卷级别打开是否与文件级别状态兼容？ 如果卷上打开了现有文件，则不允许使用独占卷打开。 这对于新开发人员来说是一个常见问题，因为他们尝试打开卷并发现它发生故障。 如果此操作失败，FSCTL\_卸除\_卷可用于使打开句柄失效并强制卸载，从而允许对新装载的卷进行独占访问。

此外，文件属性必须兼容。 无法打开具有只读属性的文件以进行写访问。 请注意，展开一般权限扩展后，应检查所需的访问权限。 例如，FASTFAT 文件系统中的这一检查是在**FatCheckFileAccess**函数中（请参阅 Acchksup 源文件，该文件来自 WDK 包含的 FASTFAT 示例）。

下面的代码示例特定于 FAT 语义。 同时还实现 Dacl 的文件系统会使用安全引用监视器例程（例如[**SeAccessCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seaccesscheck)）执行额外的安全检查。

```cpp
    //
    //  check for a read-only Dirent
    //

    if (FlagOn(DirentAttributes, FAT_DIRENT_ATTR_READ_ONLY)) {

        //
        //  Check the desired access for a read-only Dirent
        // Don't allow 
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

FASTFAT 实现的更微妙的检查是确保调用方请求的访问权限与 FAT 文件系统可识别的内容（在 Acchksup 中的**FatCheckFileAccess**函数中，该函数来自于 WDK 包含的 FASTFAT 示例）：

下面的代码示例演示了用于文件系统安全的重要概念。 检查以确保传递到文件系统的内容不在预期范围之外。 从安全角度来看，保守和正确的方法是，如果不了解访问请求，则应拒绝该请求。

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

幸运的是，对于文件系统，一旦在初始创建处理过程中完成了安全检查，则后续的安全检查由 i/o 管理器执行。 例如，i/o 管理器可以确保用户模式应用程序不会对已打开以进行读取访问的文件执行写入操作。 事实上，文件系统不应尝试对 file 对象强制实施只读语义，即使它只是为读取访问而打开的，在 IRP\_MJ\_写入调度例程。 这是由于内存管理器将特定文件对象与给定的 section 对象关联的方式造成的。 在此部分中进行的后续写入将作为 IRP\_MJ 发送到文件对象上\_写入操作，即使该文件是只读的。 换句话说，当文件句柄通过[**ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)转换为 Nt 系统服务入口点上相应的文件对象时，将执行访问权限。

在文件系统中有两个额外的位置必须与 "创建" 处理进行语义安全检查：

-   在重命名或硬链接处理期间。

-   处理文件系统控制操作时。

后续部分将讨论重命名处理和文件系统控制处理。

请注意，这并不是与 "创建" 处理相关的语义问题的详尽列表。 本部分的目的是为文件系统开发人员引起这些问题的关注。 所有语义问题都必须针对特定文件系统进行识别，实现以满足特定的语义，并经过测试，以确保实现处理各种情况。

 

 





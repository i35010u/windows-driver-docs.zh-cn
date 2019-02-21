---
title: 返回 FLT_PREOP_SYNCHRONIZE
description: 返回 FLT_PREOP_SYNCHRONIZE
ms.assetid: b1331f8d-e230-45b2-be1b-f85d85557350
keywords:
- FLT_PREOP_SYNCHRONIZE
- 同步 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63458ce3d59588f9702dd10684b1427365edb007
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543655"
---
# <a name="returning-fltpreopsynchronize"></a>返回 FLT\_PREOP\_同步


## <span id="ddk_returning_flt_preop_synchronize_if"></span><span id="DDK_RETURNING_FLT_PREOP_SYNCHRONIZE_IF"></span>


如果微筛选器驱动程序[ **preoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551109)同步 I/O 操作通过返回 FLT\_PREOP\_同步筛选器管理器调用微筛选器驱动程序[ **postoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551107)期间 I/O 完成。

筛选器管理器在 preoperation 回调，在 IRQL 与相同的线程上下文中调用微筛选器驱动程序的 postoperation 回调例程&lt;= APC\_级别。 （请注意，该线程上下文不一定是在原始线程的上下文。）

**请注意**  如果 preoperation 微筛选器驱动程序的回调例程将返回 FLT\_PREOP\_同步，但微筛选器驱动程序未注册此操作，一个 postoperation 回调例程系统断言已检验版本上。

 

如果微筛选器驱动程序的 preoperation 回调例程将返回 FLT\_PREOP\_同步，它可以返回中的非 NULL 值及其*CompletionContext*输出参数。 此参数是传递给相应的 postoperation 回调例程的可选上下文指针。 Postoperation 回调例程接收此指针在其*CompletionContext*输入的参数。

微筛选器驱动程序的 preoperation 回调例程应返回 FLT\_PREOP\_仅为基于 IRP 的 I/O 操作的同步。 但是，可针对其他操作类型返回此状态的值。 如果不是一个基于 IRP 的 I/O 操作的 I/O 操作返回它，则筛选器管理器会将此返回值，就好像 FLT\_PREOP\_成功\_WITH\_回调。 若要确定操作是否是基于 IRP 的 I/O 操作，请使用[ **FLT\_IS\_IRP\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544654)宏。

微筛选器驱动程序不应返回 FLT\_PREOP\_的同步创建的操作，因为这些操作已同步的筛选器管理器。 如果微筛选器驱动程序已注册的 IRP preoperation 和 postoperation 回调例程\_MJ\_创建操作后创建回调例程称为在 IRQL = 被动\_级别，请在同一线程上下文中预先创建的回调例程。

微筛选器驱动程序必须永远不会返回 FLT\_PREOP\_同步以进行异步读取或写入操作。 执行此操作会严重降低微筛选器驱动程序和系统性能，并可以甚至导致死锁，如果，例如，已修改的页编写器线程被阻止。 然后再返回 FLT\_PREOP\_同步的基于 IRP 的读取或写入操作，微筛选器驱动程序应验证该操作是通过调用同步[ **FltIsOperationSynchronous**](https://msdn.microsoft.com/library/windows/hardware/ff543351).

不能同步 I/O 操作的以下类型：

-   Oplock 文件系统控制 (FSCTL) 操作 (**MajorFunction**是 IRP\_MJ\_文件\_系统\_控制;**FsControlCode**是[ **FSCTL\_请求\_筛选器\_OPLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff545518)， [ **FSCTL\_请求\_批处理\_OPLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff545510)， [ **FSCTL\_请求\_OPLOCK\_级别\_1**](https://msdn.microsoft.com/library/windows/hardware/ff545538)，或[ **FSCTL\_请求\_OPLOCK\_级别\_2**](https://msdn.microsoft.com/library/windows/hardware/ff545546)。)

-   通知更改目录操作 (**MajorFunction**是 IRP\_MJ\_DIRECTORY\_控制;**MinorFunction**是 IRP\_MN\_通知\_更改\_目录。)

-   字节范围锁请求 (**MajorFunction**是 IRP\_MJ\_锁\_控制;**MinorFunction**是 IRP\_MN\_锁。)

FLT\_PREOP\_同步不能返回为上述任何操作。

 

 





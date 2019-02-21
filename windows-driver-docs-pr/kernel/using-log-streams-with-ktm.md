---
title: 日志流使用 KTM
description: 日志流使用 KTM
ms.assetid: d7ad0e16-d1f2-4c41-b647-95b5445c2708
keywords:
- 日志流 WDK KTM
- 内核事务管理器 WDK，日志流
- KTM WDK，日志流
- 常见日志文件系统 WDK 内核，KTM 日志流
- CLFS WDK 内核，KTM 日志流
- 事务管理器 WDK KTM 日志流
- 资源管理器 WDK KTM 日志流
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82766d30354f7dfe0b511da7d8fc790b87b9188c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520045"
---
# <a name="using-log-streams-with-ktm"></a>日志流使用 KTM


基于 KTM 的事务处理系统 (TPSs) 应记录事务活动通过使用[公用日志文件系统](using-common-log-file-system.md)(CLFS)。 KTM 创建事务管理器的每个对象的日志流。 每个资源管理器应创建其自己的日志流。

### <a name="creating-log-streams-for-transaction-manager-objects"></a>创建日志流的事务管理器对象

当资源管理器调用[ **ZwCreateTransactionManager**](https://msdn.microsoft.com/library/windows/hardware/ff566430)，必须指定 CLFS 日志流的名称。 如果指定的流不存在，KTM 创建它。 如果流已存在， **ZwCreateTransactionManager**重新打开它。 KTM 将此日志流分配给事务管理器对象。

KTM 使用事务管理器对象的日志流式传输到记录的事务管理器对象和所有资源管理器对象、 事务对象和登记与事务管理器对象相关联的对象的内部状态信息. 如果事务操作会中断完成前，KTM 信息可用于在日志中确定是提交还是回滚事务。

KTM 不会记录资源管理器从接收或发送到客户端的事务数据。 资源管理器必须使用其自己的日志流记录此信息。

资源管理器可以调用[ **ZwQueryInformationTransactionManager** ](https://msdn.microsoft.com/library/windows/hardware/ff567058)来获取对象的日志流，例如日志流的路径名称或 GUID 的 KTM 的事务管理器有关的信息将分配给该流。

### <a name="creating-log-streams-for-resource-managers"></a>为资源管理器中创建日志流

在其初始化代码中，每个资源管理器应调用[ **ClfsCreateLogFile** ](https://msdn.microsoft.com/library/windows/hardware/ff540792)创建其自己的日志流。 每个资源管理器应使用它的流来记录有关事务的提交、 回滚或恢复事务的数据所需的所有信息。

KTM 和 TP 的所有资源管理器可以使用单个日志文件，但每个 TP 的组件必须在日志文件中使用不同的流。 有关如何指定日志文件内的各个流的信息，请参阅[ **ClfsCreateLogFile**](https://msdn.microsoft.com/library/windows/hardware/ff540792)。

我们会定期创建 KTM[重新开始区域](reading-restart-records-from-a-clfs-stream.md)事务管理器的日志流中。 当 KTM 执行恢复操作时，它会读取最后一个的重新开始区域，恢复已关闭的情况下系统之前打开的对象的状态。 同样，资源管理器应定期在其日志的流中创建重新开始区域。 例如，资源管理器可能会创建一个重新开始区域每次完成事务的操作。

有关 CLFS 中重新开始区域的详细信息日志流，请参阅[读取重新启动记录从 CLFS Stream](reading-restart-records-from-a-clfs-stream.md)。 此外，请参阅[ **ClfsWriteRestartArea**](https://msdn.microsoft.com/library/windows/hardware/ff541770)， [ **ClfsReadRestartArea**](https://msdn.microsoft.com/library/windows/hardware/ff541709)，并[ **ClfsReadPreviousRestartArea** ](https://msdn.microsoft.com/library/windows/hardware/ff541699)例程。

### <a name="using-log-streams-for-recovery"></a>恢复使用日志流

在资源管理器调用后**ZwCreateTransactionManager**，它必须调用[ **ZwRecoverTransactionManager**](https://msdn.microsoft.com/library/windows/hardware/ff567079)。 **ZwRecoverTransactionManager**例程读取事务管理器对象的日志流恢复到已知的良好点 TP 的状态。 如果正确关闭计算机，或未关闭-上次加载的资源管理器后，日志流中所包含的最少信息。 如果发生系统故障，则日志流包含足够的恢复信息还原到已知状态的所有事务。

在资源管理器调用后[ **ZwCreateResourceManager**](https://msdn.microsoft.com/library/windows/hardware/ff566427)，它必须调用[ **ZwRecoverResourceManager**](https://msdn.microsoft.com/library/windows/hardware/ff567078)。 **ZwRecoverResourceManager**例程尝试恢复的事务的关联与每个资源管理器的登记。 有关如何恢复资源管理器的事务的详细信息，请参阅[处理恢复操作](handling-recovery-operations.md)。

### <a name="storing-transaction-data"></a>存储事务数据

CLFS 日志流所使用的资源管理器应存储中的事务数据[CLFS 封送处理区域](clfs-marshalling-areas.md)。 CLFS 定期将日志流中的数据的封送到永久存储介质的区域。 若要记录修改数据的操作，资源管理器可能会执行以下步骤：

1.  写入操作对其进行修改，到封送处理区域之前，将复制的原始数据。

2.  执行数据的副本上操作而无需修改数据库的永久存储介质。

3.  将新的数据复制到封送处理区域。

如果资源管理器收到回滚通知，它可以从日志流还原原始数据。 如果收到提交通知，资源管理器可复制修改后的数据日志流到数据库的永久存储介质。

此外可以使用资源管理器[ **ZwSetInformationEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff567094)例程来登记对象中存储恢复信息。 KTM 将此信息保存在其日志流和它从流中读取日志在恢复操作期间。 因此，资源管理器可以获取在任何时间此恢复信息，通过调用[ **ZwQueryInformationEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567051)。

 

 





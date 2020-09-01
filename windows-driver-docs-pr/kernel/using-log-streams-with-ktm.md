---
title: 将日志流与 KTM 配合使用
description: 将日志流与 KTM 配合使用
ms.assetid: d7ad0e16-d1f2-4c41-b647-95b5445c2708
keywords:
- 日志流 WDK KTM
- 内核事务管理器 WDK，日志流
- KTM WDK，日志流
- 公用日志文件系统 WDK 内核，KTM 日志流
- CLFS WDK 内核，KTM 日志流
- 事务管理器 WDK KTM，日志流
- 资源管理器 WDK KTM，日志流
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bc363b56feecddbdc3cac4aba2c5e435418bd7b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188201"
---
# <a name="using-log-streams-with-ktm"></a>将日志流与 KTM 配合使用


基于 KTM 的事务处理系统 (TPSs) 应使用 [公用日志文件系统](using-common-log-file-system.md) (CLFS) 记录事务活动。 KTM 为每个事务管理器对象创建日志流。 每个资源管理器都应创建自己的日志流。

### <a name="creating-log-streams-for-transaction-manager-objects"></a>为事务管理器对象创建日志流

当资源管理器调用 [**ZwCreateTransactionManager**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransactionmanager)时，必须指定 CLFS 日志流的名称。 如果指定的流不存在，则 KTM 会创建它。 如果流已存在， **ZwCreateTransactionManager** 将重新打开它。 KTM 将此日志流分配给事务管理器对象。

KTM 使用事务管理器对象的日志流来记录有关事务管理器对象以及与事务管理器对象关联的所有资源管理器对象、事务对象和登记对象的内部状态信息。 如果事务操作在完成之前中断，则 KTM 可以使用日志中的信息来确定是提交还是回滚事务。

KTM 不会记录资源管理器从客户端接收或发送到客户端的事务数据。 资源管理器必须使用自己的日志流来记录此信息。

资源管理器可以调用 [**ZwQueryInformationTransactionManager**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationtransactionmanager) 来获取事务管理器对象的日志流的相关信息，例如日志流的路径名称或 KTM 分配给该流的 GUID。

### <a name="creating-log-streams-for-resource-managers"></a>为资源管理器创建日志流

在其初始化代码中，每个资源管理器都应调用 [**ClfsCreateLogFile**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatelogfile) 来创建其自己的日志流。 每个资源管理器都应该使用其流来记录有关其提交、回滚或恢复事务数据所需的事务的所有信息。

一个 TPS 和一个 TPS 的所有资源管理器都可以使用一个日志文件，但每个 TPS 组件必须在该日志文件中使用不同的流。 有关如何在日志文件中指定单个流的信息，请参阅 [**ClfsCreateLogFile**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatelogfile)。

KTM 会定期在事务管理器的日志流中创建一个 [重启区域](reading-restart-records-from-a-clfs-stream.md) 。 当 KTM 执行恢复操作时，它将读取上次重新启动区域，以恢复在系统关闭之前已打开的对象的状态。 同样，资源管理器应定期在其日志流中创建重新启动区域。 例如，资源管理器可能会在每次完成事务操作时创建一个重启区域。

有关 CLFS 日志流中重新启动区域的详细信息，请参阅 [读取 CLFS 流中的重新启动记录](reading-restart-records-from-a-clfs-stream.md)。 另请参阅 [**ClfsWriteRestartArea**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfswriterestartarea)、 [**ClfsReadRestartArea**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadrestartarea)和 [**ClfsReadPreviousRestartArea**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadpreviousrestartarea) 例程。

### <a name="using-log-streams-for-recovery"></a>使用日志流进行恢复

资源管理器调用 **ZwCreateTransactionManager**后，必须调用 [**ZwRecoverTransactionManager**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecovertransactionmanager)。 **ZwRecoverTransactionManager**例程读取事务管理器对象的日志流，以将该 TPS 的状态恢复到已知的正确点。 如果计算机在资源管理器上一次加载后正确关闭或未关闭，则日志流包含最少的信息。 如果发生系统崩溃，日志流将包含足够的恢复信息，以将所有事务还原到已知状态。

资源管理器调用 [**ZwCreateResourceManager**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateresourcemanager)后，必须调用 [**ZwRecoverResourceManager**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverresourcemanager)。 **ZwRecoverResourceManager**例程尝试恢复与每个资源管理器的登记关联的事务。 有关如何恢复资源管理器的事务的详细信息，请参阅 [处理恢复操作](handling-recovery-operations.md)。

### <a name="storing-transaction-data"></a>存储事务数据

使用 CLFS 日志流的资源管理器应将事务数据存储在 [CLFS 封送区](clfs-marshalling-areas.md)。 CLFS 定期将数据从日志流的封送处理区移动到永久性存储介质。 若要记录修改数据的操作，资源管理器可以执行以下操作：

1.  在写入操作将其修改为封送处理区之前，复制原始数据。

2.  对数据副本执行操作，而不修改数据库的永久存储介质。

3.  将新数据复制到 "封送" 区域。

如果资源管理器收到回滚通知，则它可以从日志流还原原始数据。 如果它收到提交通知，则资源管理器可以将修改后的数据从日志流复制到数据库的永久存储介质。

资源管理器还可以使用 [**ZwSetInformationEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsetinformationenlistment) 例程将恢复信息存储在登记对象中。 KTM 会将此信息保存在其日志流中，并在恢复操作期间从日志流中读取此信息。 因此，资源管理器可以通过调用 [**ZwQueryInformationEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationenlistment)随时获取此恢复信息。

 


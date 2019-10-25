---
title: 创建资源管理器
description: 创建资源管理器
ms.assetid: b2841d56-650a-487c-a002-2521cd1b461b
keywords:
- 资源管理器 WDK KTM，创建资源管理器
- 登记 WDK KTM，只读登记
- 只读登记 WDK KTM
- 资源管理器 WDK KTM，可变资源管理器
- 可变资源管理器 WDK KTM
- 资源管理器 WDK KTM，添加到 TPS
- 事务处理系统 WDK KTM，添加资源管理器
- TPS WDK KTM，添加资源管理器
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d152ede92254bf463182300c9a9c2f6c167b6669
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837022"
---
# <a name="creating-a-resource-manager"></a>创建资源管理器


[*资源管理器*](transaction-processing-terms.md#ktm-term-resource-manager)维护每个事务的数据，并记录事务的操作。 如果事务处理系统（TPS）有多个资源管理器，则每个资源管理器都可以参与每个事务的提交、回滚和恢复操作。

每个资源管理器都必须导出一个接口，事务客户端可以使用该接口访问资源管理器维护的数据库或其他资源。

通常，内核模式资源管理器必须按列出的顺序执行以下任务：

1.  创建日志流。

    资源管理器可以使用[公用日志文件系统](using-common-log-file-system.md)（CLFS）或其他一些日志记录功能来维护其日志流。 调用[**ClfsCreateLogFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatelogfile)会创建 CLFS 日志流。 资源管理器必须使用日志流记录其提交、回滚或恢复事务所需的任何信息。 此外，KTM 使用日志流记录可能需要恢复事务的任何内部状态更改。

2.  创建事务管理器对象。

    调用[**ZwCreateTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransactionmanager)会创建事务管理器对象，并将资源管理器连接到资源管理器指定的附加 CLFS 日志流。

3.  恢复事务管理器状态。

    对[**ZwRecoverTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecovertransactionmanager)的调用读取事务管理器对象的日志流（该对象是 KTM 维护的），并确定是否在完成所有事务（例如因为系统崩溃）之前关闭 TPS。 KTM 根据日志流中的信息还原其内部状态。

4.  创建资源管理器对象。

    对[**ZwCreateResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateresourcemanager)的调用会创建资源管理器对象，并将其与之前创建的事务管理器对象关联。

5.  恢复资源管理器状态。

    对[**ZwRecoverResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverresourcemanager)的调用会导致 KTM 发送 RESOURCE manager 事务\_通知在资源管理器上次关闭时正在进行的任何事务的\_恢复通知。 有关资源管理器应如何响应这些通知的信息，请参阅[处理恢复操作](handling-recovery-operations.md)。

6.  接收来自客户端的事务。

    通常，客户端会创建一个事务对象，并使用资源管理器的客户端接口将该事务对象的 GUID 传递到 resource manager。 例如，资源管理器可能会提供类似于 "[理解 TPS 组件](understanding-tps-components.md)" 主题所描述的*CreateDataObject*例程。

7.  在每个事务中登记。

    对[**ZwOpenTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopentransaction)的调用会打开事务对象的句柄，然后对[**ZwCreateEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateenlistment)的调用会为事务创建登记。 通过登记，资源管理器可以接收指定的[事务通知](transaction-notifications.md)集。

8.  启用事务通知的接收。

    资源管理器可以调用[**ZwGetNotificationResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntgetnotificationresourcemanager)来同步获取通知，也可以调用[**TmEnableCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmenablecallbacks)来注册一个*ResourceManagerNotification*回调例程，只要通知可用。

9.  来自客户端的服务资源访问请求，但不将更改永久更改。

    在客户端创建事务对象之后，它通常会调用资源管理器的接口来访问资源管理器的资源。 例如，数据库的资源管理器可能会收到对数据库的读取和写入请求。

    资源管理器必须在[CLFS 日志流](using-log-streams-with-ktm.md)或其他日志记录功能中记录读和写操作的结果，直到收到通知，指出事务的操作将提交、回滚或恢复。

10. 提交或回滚客户端操作。

    最终，资源管理器会收到通知，以开始提交或回滚客户端已执行的操作。 在响应中，资源管理器必须使客户端操作永久永久性或丢弃它们。 有关如何处理提交和回滚通知的详细信息，请参阅[处理事务操作](handling-transaction-operations.md)。

    有时，资源管理器可能必须尝试强制 KTM 快速提供提交或回滚通知，原因可能是资源管理器已确定设备已被意外删除。 在这种情况下，资源管理器可以调用[**TmRequestOutcomeEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmrequestoutcomeenlistment)。

11. 关闭登记对象句柄。

    资源管理器处理完事务之后，必须调用[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)来关闭登记对象的句柄

12. 关闭 resource manager 对象句柄和事务管理器对象句柄。

    在资源管理器卸载之前，必须调用[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)来关闭 resource manager 对象的句柄和事务管理器对象的句柄。

必须在资源管理器的初始化代码中执行步骤1到步骤5。 例如，如果资源管理器是内核模式驱动程序，则初始化代码是驱动程序的[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程。

步骤6到11通常在对事务客户端请求作出响应的代码中执行。

步骤12必须在资源管理器的最终清理代码（如内核模式驱动程序的[*卸载*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)例程）中执行。

## <a href="" id="kernel-creating-a-read-only-enlistment"></a>创建只读登记


*只读登记*是不接收来自 KTM 的任何通知的登记。 资源管理器可以通过调用[**ZwReadOnlyEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntreadonlyenlistment)使任何登记成为只读的。 此调用会导致 KTM 停止向资源管理器发送通知。

资源管理器调用[**ZwCreateEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateenlistment)后，就可以在任何时候调用**ZwReadOnlyEnlistment** ，直到通常调用[**ZwPrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreparecomplete)。

你可能希望资源管理器调用**ZwReadOnlyEnlistment**的原因有两个。

-   资源管理器已参与事务，并且在收到事务\_通知\_提交通知时，资源管理器将确定不再需要参与事务的提交运作.

    例如，当 resource manager 收到事务\_通知\_准备通知时，它可能会确定事务的所有操作都没有更改资源管理器的数据库。 资源管理器可以调用**ZwReadOnlyEnlistment**而不是**ZwPrepareComplete** ，将其自身从事务中删除。

-   资源管理器从不参与任何事务的提交操作。

    例如，资源管理器可能会监视客户端发送的数据，而不修改任何存储的数据库。 在这种情况下，资源管理器可能会在调用**ZwCreateEnlistment**后立即调用**ZwReadOnlyEnlistment** 。 此外，你可以选择使此类资源管理器*可变*，如本主题的下一部分中所述。

资源管理器调用**ZwReadOnlyEnlistment**后，可以调用[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)来关闭登记句柄。

## <a href="" id="kernel-creating-a-volatile-resource-manager"></a>创建可变资源管理器


*可变资源管理器*是不维护持久数据的资源管理器。 例如，如果资源管理器未修改持久存储的数据库，则可以创建一个可变资源管理器来监视客户端发送的数据。 可变资源管理器通常不记录事务活动，因此不能执行恢复或回滚操作。

可变资源管理器在调用[**ZwCreateResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateresourcemanager)时必须将资源\_管理器设置\_可变标志。 如果设置此标志，则 KTM 不会记录有关关联的事务管理器对象的日志流中的资源管理器的任何信息。

在调用[**ZwCreateTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransactionmanager)时，资源管理器还可以设置事务\_MANAGER\_可变标志。 如果设置了此标志，则 KTM 不会为事务管理器对象创建日志流。 此外，连接到事务管理器对象的任何其他资源管理器也必须是可变的，并将资源\_管理器设置\_可变标志。

## <a name="adding-a-resource-manager-to-an-existing-tps"></a>向现有 TPS 添加资源管理器


如果必须将其他资源管理器添加到现有 TPS，则有两个选择：

-   新资源管理器调用[**ZwCreateTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransactionmanager)来创建其自己的事务管理器对象。

    如果资源管理器不与 TPS 中的其他资源管理器通信，请使用此选项。

-   新资源管理器调用[**ZwOpenTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopentransactionmanager)连接到现有的事务管理器对象。

    如果资源管理器必须与 TPS 中的其他资源管理器通信，请使用此选项。 调用**ZwCreateTransactionManager**的资源管理器必须共享事务管理器对象的 GUID、日志流名称或对象名称，以便其他资源管理器可以调用**ZwOpenTransactionManager**。 这些其他资源管理器可以调用[**ZwQueryInformationTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationtransactionmanager)来获取有关事务管理器对象的其他信息。

在将资源管理器添加到 TPS 后，知道资源管理器的客户端可以调用 resource manager 的客户端接口。

 

 





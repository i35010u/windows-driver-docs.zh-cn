---
title: SPB I/O 请求
description: 这些 IOCTLs 由控制器驱动程序处理 (外围设备驱动程序) 的客户端发送。
ms.date: 11/29/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94c971dad2ae59468e8b14027a9d6865adce3622
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811821"
---
# <a name="spb-io-requests"></a>SPB I/O 请求

系统提供的 CTL_CODE 宏在定义 i/o 控制代码中进行了介绍，用于定义 Spb 中的 IOCTL_SPB_ * 控制代码。

|主题 | 描述|
|------|:----------------|
|[IOCTL_SPB_EXECUTE_SEQUENCE](#ioctl_spb_execute_sequence) | IOCTL_SPB_EXECUTE_SEQUENCE i/o 控制代码使客户端 (的外围设备驱动程序) 使用 SPB 控制器驱动程序，以执行一系列传输 (读取和写入) 作为一个 i/o 请求的单个原子操作。 总线上指定的设备是序列中所有传输的目标。|
|[IOCTL_SPB_FULL_DUPLEX](#ioctl_spb_full_duplex-control-code) | IOCTL_SPB_FULL_DUPLEX 控制代码由客户端 (外设驱动程序) 用于请求全双工 i/o 操作。 对于可以同时读取和写入数据的总线（如 SPI），控制器支持全双工 i/o 操作。|
|[IOCTL_SPB_LOCK_CONNECTION](#ioctl_spb_lock_connection-control-code) | IOCTL_SPB_LOCK_CONNECTION 控制代码由客户端 (外设驱动程序) ，以获取与另一个客户端共享的已连接到 SPB 的目标设备上的连接锁。 当客户端持有连接锁时，此客户端具有对设备的独占访问权限。|
|[IOCTL_SPB_LOCK_CONTROLLER](#ioctl_spb_lock_controller-control-code) | IOCTL_SPB_LOCK_CONTROLLER 控制代码由客户端 (外设驱动程序) 用于锁定 SPB 控制器。 控制器锁定时，客户端会独占使用总线来访问指定的目标设备进行锁定。
|[IOCTL_SPB_UNLOCK_CONNECTION](#ioctl_spb_unlock_connection-control-code) | I/o 控制代码由客户端使用 (外设驱动程序) ，以释放与其他客户端共享的连接到 SPB 的目标设备上的连接锁。 客户端之前发送了 IOCTL_SPB_LOCK_CONNECTION 请求以获取设备的独占访问权限。|
|[IOCTL_SPB_UNLOCK_CONTROLLER](#ioctl_spb_unlock_controller-control-code) |IOCTL_SPB_UNLOCK_CONTROLLER i/o 控制代码由客户端 (外设驱动程序) 用于解锁 SPB 控制器。 客户端以前锁定了控制器，以独占使用总线来访问总线上的目标设备。|

## <a name="ioctl_spb_execute_sequence"></a>IOCTL_SPB_EXECUTE_SEQUENCE

IOCTL_SPB_EXECUTE_SEQUENCE i/o 控制代码使客户端 (的外围设备驱动程序) 使用 SPB 控制器驱动程序，以执行一系列传输 (读取和写入) 作为一个 i/o 请求的单个原子操作。 总线上指定的设备是序列中所有传输的目标。

通过将固定长度传输序列指定为单个原子操作，IOCTL_SPB_EXECUTE_SEQUENCE i/o 控制请求使控制器驱动程序能够优化 i/o 传输并提高性能。

客户端将此 i/o 控制请求发送到目标设备的文件对象。

SPB 控制器驱动程序注册一个 EvtSpbControllerIoSequence 回调函数以执行 i/o 传输序列的总线传输。 SPB framework 扩展 (SpbCx) 调用此函数将 IOCTL_SPB_EXECUTE_SEQUENCE 请求传递到 SPB 控制器驱动程序进行处理。

### <a name="input-buffer"></a>输入缓冲区

输入缓冲区是 SPB_TRANSFER_LIST 结构，它包含指向客户端数据缓冲区的指针的列表。 此列表包含每个传输 (在 i/o 传输序列中读取或写入) 的数据缓冲区。

### <a name="input-buffer-length"></a>输入缓冲区长度

SPB_TRANSFER_LIST 结构的大小。

### <a name="status-block"></a>状态块

如果操作成功，则控制器驱动程序会将状态成员设置为 STATUS_SUCCESS，并将信息成员设置为在序列过程中传输的总字节数。

此操作可能会因各种原因而失败，其中可能包括资源不足、客户端输入无效以及设备故障。

如果控制器驱动程序开始处理 i/o 请求，但在序列中的某个传输过程中发生错误 (例如，目标设备向 NACK 发出信号以拒绝传输) ，控制器驱动程序将中止序列中剩余的传输。 然后，该驱动程序将完成状态设置为 STATUS_SUCCESS，将信息成员设置为发生错误之前已成功传输的字节数，并完成请求。

## <a name="ioctl_spb_full_duplex-control-code"></a>IOCTL_SPB_FULL_DUPLEX 控制代码

IOCTL_SPB_FULL_DUPLEX 控制代码由客户端 (外设驱动程序) 用于请求全双工 i/o 操作。 对于可以同时读取和写入数据的总线（如 SPI），控制器支持全双工 i/o 操作。
定义 i/o 控制代码时，系统提供的 CTL_CODE 宏用于定义 IOCTL_SPB_FULL_DUPLEX，如下所示。

总线上设备的用户模式驱动程序或内核模式驱动程序将此 i/o 控制请求发送到目标设备的文件对象。

此 IOCTL 仅支持用于总线的 SPB 控制器驱动程序，如 SPI，可以同时读取和写入数据。

全双工传输的写入和读取缓冲区由 SPB_TRANSFER_LIST 结构描述。 此结构必须使用以下格式：

* SPB_TRANSFER_LIST_ENTRY 结构的数组只包含两个元素。 第一个元素描述写入缓冲区 (Direction = SpbTransferDirectionToDevice) 。 第二个元素描述读取缓冲区 (Direction = SpbTransferDirectionFromDevice) 。
* 两个 SPB_TRANSFER_LIST_ENTRY 结构的 DelayInUs 成员必须为零。 写入缓冲区和读取缓冲区的缓冲区格式可以是以下任一项：

  * SpbTransferBufferFormatSimple
  * SpbTransferBufferFormatList
  * SpbTransferBufferFormatSimpleNonPaged
  * SpbTransferBufferFormatMdl

  前面的列表中的最后两种格式只能由内核模式客户端使用。 写入和读取缓冲区的格式不必相同。 有关这些缓冲区格式的详细信息，请参阅 SPB_TRANSFER_BUFFER_FORMAT。

成功的操作可能会将信息成员的值设置为小于写入缓冲区和读取缓冲区的大小之和的值，如果请求被取消，则可能会发生这种情况，或者如果操作无法将写入缓冲区的全部内容写入设备，或使用从设备读取的数据完全填充读取缓冲区。

写入和读取缓冲区的大小不必相同。 如果写入缓冲区大于读取缓冲区，则操作将在读取缓冲区已满后继续从写入缓冲区写入数据。 如果读取缓冲区大于写入缓冲区，则在清空写入缓冲区后，操作将继续填充读取缓冲区。

如果 SPB 控制器驱动程序注册了一个 EvtSpbControllerIoOther 回调函数，则 SPB framework 扩展 (SpbCx) 调用此函数将 IOCTL_SPB_FULL_DUPLEX 请求传递到 SPB 控制器驱动程序进行处理。 SpbCx 不执行任何参数检查、传输列表验证或 IOCTL_SPB_FULL_DUPLEX 请求的其他处理。

有关 SPB 控制器驱动程序如何为此 IOCTL 实现支持的详细信息，请参阅处理 IOCTL_SPB_FULL_DUPLEX 请求。

### <a name="input-buffer"></a>输入缓冲区

指向 SPB_TRANSFER_LIST 结构的指针，该结构包含指向客户端输入和输出数据缓冲区的指针。 此结构只包含两个元素的传输数组。 第一个元素描述包含要写入设备的数据的缓冲区。 第二个元素描述用于保存从设备读取的数据的缓冲区。
有关 SPB 控制器驱动程序如何实现 (IOCTL) 请求的自定义 i/o 控件的详细信息，该控件使用 SPB_TRANSFER_LIST 结构来描述缓冲区，请参阅使用自定义 IOCTLs 的 SPB_TRANSFER_LIST 结构。

### <a name="input-buffer-length"></a>输入缓冲区长度

SPB_TRANSFER_LIST 结构的大小。

### <a name="status-block"></a>状态块

如果操作成功，则控制器驱动程序会将状态成员设置为 STATUS_SUCCESS，并将信息成员设置为传输的字节总数（ (读取字节数）以及全双工操作期间写入) 字节数。

此操作可能会因各种原因而失败，其中可能包括资源不足、客户端输入无效以及设备故障。

## <a name="ioctl_spb_lock_connection-control-code"></a>IOCTL_SPB_LOCK_CONNECTION 控制代码

IOCTL_SPB_LOCK_CONNECTION 控制代码由客户端 (外设驱动程序) ，以获取与另一个客户端共享的已连接到 SPB 的目标设备上的连接锁。 当客户端持有连接锁时，此客户端具有对设备的独占访问权限。
定义 i/o 控制代码时，系统提供的 CTL_CODE 宏用于定义 IOCTL_SPB_LOCK_CONNECTION，如下所示。

IOCTL_SPB_LOCK_CONNECTION 和 IOCTL_SPB_UNLOCK_CONNECTION 请求获取并释放连接到简单外围总线的目标设备上的连接锁。 大多数客户端不使用这些 i/o 控制请求。 仅当两个客户端共享对同一目标设备的访问时，才使用这些请求。 有关详细信息，请参阅 SPB 连接锁。

两个客户端可以打开到同一目标设备的单独逻辑连接，并在客户端要求独占访问设备时使用连接锁定。 当一台客户端持有锁定时，从第二个客户端到设备的 i/o 请求会自动延迟，直到第一个客户端释放该锁。

客户端可以同时在目标设备上持有连接锁，在 SPB 控制器上保存控制器锁。 IOCTL_SPB_LOCK_CONTROLLER 和 IOCTL_SPB_UNLOCK_CONTROLLER 请求获取并释放控制器锁。 客户端必须在获取控制器锁之前获取连接锁，并且必须释放控制器锁才能释放连接锁。 客户端使用控制器锁来执行一组有序的总线传输 (读取和写入操作) 为单个原子总线操作。 有关详细信息，请参阅 i/o 传输序列。

如果在设备上锁定连接时向目标设备发送 IRP_MJ_CLEANUP 请求，则会自动终止连接锁。 当客户端将其文件句柄关闭到设备时，会将清理请求发送到该目标设备。

### <a name="status-block"></a>状态块

如果操作成功，则状态成员设置为 STATUS_SUCCESS。

如果操作失败，状态成员将设置为适当的错误状态代码。

如果客户端已持有目标设备上的连接锁或 SPB 控制器上的控制器锁定，此操作将失败，状态为 "STATUS_INVALID_DEVICE_REQUEST"。 此操作可能因其他原因而失败，其中可能包括资源不足、客户端输入无效以及设备故障。

## <a name="ioctl_spb_lock_controller-control-code"></a>IOCTL_SPB_LOCK_CONTROLLER 控制代码

IOCTL_SPB_LOCK_CONTROLLER 控制代码由客户端 (外设驱动程序) 用于锁定 SPB 控制器。 控制器锁定时，客户端会独占使用总线来访问指定的目标设备进行锁定。
定义 i/o 控制代码时，系统提供的 CTL_CODE 宏用于定义 IOCTL_SPB_LOCK_CONTROLLER，如下所示。

若要独占使用总线访问目标设备， (外围设备驱动程序的客户端) 将此 IOCTL 发送到目标的文件对象。 此 IOCTL 完成后，控制器将被锁定，并且所有 i/o 传输 (在总线上访问指定的目标) 。 在传输之间，控制器会保持目标设备处于选中状态，但会停止时钟。

控制器保持锁定状态，直到客户端发送 IOCTL_SPB_UNLOCK_CONTROLLER 请求来解锁控制器。 当客户端在目标设备上进行的传输序列完成时，客户端必须解锁控制器，以便控制器可以处理总线上其他目标的 i/o 请求。

如果在目标设备上锁定控制器时向目标设备发送 IRP_MJ_CLEANUP 请求，则会自动终止锁定。 当客户端关闭目标的句柄时，将向目标发送一个清除请求。

SPB 控制器不需要支持 IOCTL_SPB_LOCK_CONTROLLER 和 IOCTL_SPB_UNLOCK_CONTROLLER 请求，外围设备驱动程序不应假定它们受支持。

如果 SPB 控制器驱动程序注册了一个 EvtSpbControllerLock 回调函数，则 SPB framework 扩展 (SpbCx) 调用此函数将 IOCTL_SPB_LOCK_CONTROLLER 请求传递到 SPB 控制器驱动程序进行处理。

### <a name="status-block"></a>状态块

如果操作成功，则状态成员设置为 STATUS_SUCCESS。
此 IOCTL 可能会出于多种原因而返回错误状态，包括将控制器配置为在独占访问模式下操作失败。 在此模式下，控制器会保持选择目标设备，使其成为总线上所有 i/o 传输的独占目标。 控制器将保持此模式，直到解锁。

## <a name="ioctl_spb_unlock_connection-control-code"></a>IOCTL_SPB_UNLOCK_CONNECTION 控制代码

IOCTL_SPB_UNLOCK_CONNECTION i/o 控制代码由客户端 (外设驱动程序) 用于在与其他客户端共享的已连接到 SPB 的目标设备上释放连接锁。 客户端之前发送了 IOCTL_SPB_LOCK_CONNECTION 请求以获取设备的独占访问权限。

IOCTL_SPB_LOCK_CONNECTION 和 IOCTL_SPB_UNLOCK_CONNECTION 请求获取并释放连接到简单外围总线的目标设备上的连接锁。 大多数客户端不使用这些 i/o 控制请求。 仅当两个客户端共享对同一目标设备的访问时，才使用这些请求。 有关详细信息，请参阅 SPB 连接锁。

在客户端 (外围设备驱动程序) 将 IOCTL_SPB_LOCK_CONNECTION 请求发送到总线上的目标设备，并且请求成功完成后，连接将保持锁定状态，直到客户端发送 IOCTL_SPB_UNLOCK_CONNECTION 请求来解锁连接。

当客户端不再需要对设备的独占访问权限时，客户端将发送一个 IOCTL_SPB_UNLOCK_CONNECTION 请求，以释放目标设备的连接锁。 必须解锁连接，以便其他客户端可以访问设备。

### <a name="status-block"></a>状态块

如果操作成功，则状态成员设置为 STATUS_SUCCESS。

如果操作失败，状态成员将设置为适当的错误状态代码。 如果客户端未在目标设备上持有连接锁，或者客户端仍在 SPB 控制器上持有连接锁，此操作将失败，状态为 "STATUS_INVALID_DEVICE_REQUEST"。 此操作可能因其他原因而失败，其中可能包括资源不足、客户端输入无效以及设备故障。

## <a name="ioctl_spb_unlock_controller-control-code"></a>IOCTL_SPB_UNLOCK_CONTROLLER 控制代码

IOCTL_SPB_UNLOCK_CONTROLLER i/o 控制代码由客户端 (外设驱动程序) 用于解锁 SPB 控制器。 客户端以前锁定了控制器，以独占使用总线来访问总线上的目标设备。

在客户端 (外围设备驱动程序) 将 IOCTL_SPB_LOCK_CONTROLLER i/o 控制请求发送到总线上的目标设备后，控制器会保持锁定状态，直到客户端发送 IOCTL_SPB_UNLOCK_CONTROLLER i/o 控制请求来解锁控制器。 客户端将这些 i/o 控制请求发送到目标设备的文件对象。

当客户端在总线上完成一系列传输并想要释放目标设备时，将发送 IOCTL_SPB_UNLOCK_CONTROLLER 请求。 必须解除控制器锁定，以便它可以处理总线上其他目标的 i/o 请求。

SPB 控制器不需要支持 IOCTL_SPB_LOCK_CONTROLLER 和 IOCTL_SPB_UNLOCK_CONTROLLER 请求，外围设备驱动程序不应假定它们受支持。

SPB framework 扩展 (SpbCx) 调用 SPB 控制器驱动程序的可选 EvtSpbControllerUnlock 回调函数，以将 IOCTL_SPB_LOCK_CONTROLLER 请求传递到 SPB 控制器驱动程序进行处理。

## <a name="status-block"></a>状态块

如果操作成功，则状态成员设置为 STATUS_SUCCESS。
此 IOCTL 仅在以下情况下才会失败：未将控制器锁定为独占访问指定目标的客户端。

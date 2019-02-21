---
title: 存储 I/O 请求
description: 这些 Ioctl 发送由控制器驱动程序处理的客户端 （外围设备驱动程序）。
ms.assetid: 4b8ed75e-1f03-4b7a-ad9d-0dfa9b20274c
ms.date: 11/29/2017
ms.localizationpriority: medium
ms.openlocfilehash: 019da4445482ffffe61e6117e0d17eff1a478ce4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542253"
---
# <a name="spb-io-requests"></a>存储 I/O 请求
系统提供 CTL_CODE 宏，这定义 I/O 控制代码中所述，用于定义在 Spb.h IOCTL_SPB_ * 控制代码。

|主题 | 描述|
|------|:----------------|
|[IOCTL_SPB_EXECUTE_SEQUENCE](#ioctl-spb-execute-sequence) | IOCTL_SPB_EXECUTE_SEQUENCE I/O 控制代码允许客户端 （外围设备驱动程序） 的存储控制器驱动程序执行一系列传输 （读取和写入） 作为一个原子操作与一个 I/O 请求。 总线上指定的设备是序列中的所有传输的目标。|
|[IOCTL_SPB_FULL_DUPLEX](#ioctl-spb-full-duplex) | IOCTL_SPB_FULL_DUPLEX 控制代码由客户端 （外围设备驱动程序） 用于请求全双工 I/O 操作。 例如，可以同时读取和写入数据的 SPI 总线控制器支持全双工 I/O 操作。|
|[IOCTL_SPB_LOCK_CONNECTION](#ioctl-spb-lock-connection) | 客户端 （外围设备驱动程序） 使用 IOCTL_SPB_LOCK_CONNECTION 控制代码获取与另一个客户端共享的存储连接的目标设备上的连接锁。 在连接锁保留客户端，此客户端可以独占访问设备。|
|[IOCTL_SPB_LOCK_CONTROLLER](#ioctl-spb-lock-controller) | 客户端 （外围设备驱动程序） 使用 IOCTL_SPB_LOCK_CONTROLLER 控制代码锁定存储控制器。 虽然控制器处于锁定状态，客户端具有独占使用总线访问指定的目标设备的锁。
|[IOCTL_SPB_UNLOCK_CONNECTION](#ioctl-spb-unlock-connection) | 客户端 （外围设备驱动程序） 使用的 I/O 控制代码来释放与另一个客户端共享的存储连接的目标设备上的连接锁。 客户端先前所发送的 IOCTL_SPB_LOCK_CONNECTION 请求以独占方式访问设备。|
|[IOCTL_SPB_UNLOCK_CONTROLLER](#ioctl-spb-unlock-controller) |客户端 （外围设备驱动程序） 用 IOCTL_SPB_UNLOCK_CONTROLLER I/O 控制代码来解锁存储控制器。 客户端在之前锁定以获得独占使用的总线访问总线上的目标设备的控制器。|

## <a href='#ioctl-spb-execute-sequence' id='ioctl-spb-execute-sequence'>IOCTL_SPB_EXECUTE_SEQUENCE</a>

IOCTL_SPB_EXECUTE_SEQUENCE I/O 控制代码允许客户端 （外围设备驱动程序） 的存储控制器驱动程序执行一系列传输 （读取和写入） 作为一个原子操作与一个 I/O 请求。 总线上指定的设备是序列中的所有传输的目标。

通过指定为单个原子操作的一系列固定长度传输，IOCTL_SPB_EXECUTE_SEQUENCE I/O 控制请求，控制器驱动程序来优化 I/O 传输并提高性能。

客户端将此 I/O 控制请求发送到目标设备的文件对象。

存储控制器驱动程序注册为一个 I/O 传输序列执行总线传输 EvtSpbControllerIoSequence 回调函数。 存储框架扩展 (SpbCx) 调用此函数可将 IOCTL_SPB_EXECUTE_SEQUENCE 请求传递给处理的存储控制器驱动程序。

### <a name="input-buffer"></a>输入缓冲区
输入的缓冲区是 SPB_TRANSFER_LIST 结构，其中包含指向客户端的数据缓冲区的指针的列表。 此列表包含个 I/O 传输序列的每次传输 （读取或写入） 数据缓冲区。
### <a name="input-buffer-length"></a>输入缓冲区长度
SPB_TRANSFER_LIST 结构的大小。

### <a name="status-block"></a>状态块
如果操作成功，控制器驱动程序的状态成员设置为 STATUS_SUCCESS，和的信息成员设置为在序列期间传输的字节总数。

出于各种原因，可以包含的资源不足、 无效的客户端输入和设备工作不正常情况下，此操作可能会失败。

如果控制器驱动程序开始处理 I/O 请求，但其中一个序列中传输过程中发生错误 （例如，目标设备信号 NACK 拒绝传输），该控制器驱动程序中止序列中其余的传输。 然后，驱动程序将完成状态设置为 STATUS_SUCCESS，信息成员设置为错误发生，并完成请求之前已成功传输的字节数。

## <a href='#ioctl-spb-full-duplex' id='ioctl-spb-full-duplex'>IOCTL_SPB_FULL_DUPLEX 控制代码</a>

IOCTL_SPB_FULL_DUPLEX 控制代码由客户端 （外围设备驱动程序） 用于请求全双工 I/O 操作。 例如，可以同时读取和写入数据的 SPI 总线控制器支持全双工 I/O 操作。
系统提供 CTL_CODE 宏，这定义 I/O 控制代码中所述，用于定义 IOCTL_SPB_FULL_DUPLEX，如下所示。

用户模式驱动程序或设备总线上的内核模式驱动程序将此 I/O 控制请求发送到目标设备的文件对象。

此 IOCTL 仅受总线，例如 SPI，可读取和写入数据，同时存储控制器驱动程序。

由 SPB_TRANSFER_LIST 结构描述全双工传输的写入和读取缓冲区。 此结构必须使用以下格式：
- SPB_TRANSFER_LIST_ENTRY 结构数组包含两个元素。 第一个元素描述写入缓冲区 (方向 = SpbTransferDirectionToDevice)。 第二个元素描述读取的缓冲区 (方向 = SpbTransferDirectionFromDevice)。
- 两个 SPB_TRANSFER_LIST_ENTRY 结构 DelayInUs 成员必须为零。
  写入缓冲区和读取的缓冲区的缓冲区格式可以是以下任一项：
  -    SpbTransferBufferFormatSimple
  -    SpbTransferBufferFormatList
  -    SpbTransferBufferFormatSimpleNonPaged
  -    上面的列表中的最后两个 SpbTransferBufferFormatMdl 格式仅内核模式下客户端使用。 用于写入和读取缓冲区的格式不需要是相同的。 有关这些缓冲区格式的详细信息，请参阅 SPB_TRANSFER_BUFFER_FORMAT。

成功的操作可能会将信息成员设置为一个值小于写入缓冲区的大小的总和，并读取缓冲区，而这可能会取消该请求，或者如果该操作不能将写入缓冲区的全部内容写入设备或完全填充从设备读取的数据读取的缓冲区。

写入和读取缓冲区大小不需要是相同的。 如果写入缓冲区的大小比读取缓冲区大小，该操作会继续将数据从写入缓冲区写入后读取的缓冲区已满。 如果读取的缓冲区的大小比写入缓冲区大小，该操作将继续填充读取的缓冲区后清空写入缓冲区。

如果存储控制器驱动程序注册 EvtSpbControllerIoOther 回调函数，则存储 framework 扩展 (SpbCx) 将调用此函数可将 IOCTL_SPB_FULL_DUPLEX 请求传递给处理的存储控制器驱动程序。 SpbCx 不 IOCTL_SPB_FULL_DUPLEX 请求执行任何参数检查、 传输列表验证或其他处理。

有关如何存储控制器驱动程序实现对此 IOCTL 的支持的详细信息，请参阅处理 IOCTL_SPB_FULL_DUPLEX 请求。

### <a name="input-buffer"></a>输入缓冲区
指向 SPB_TRANSFER_LIST 结构，其中包含客户端的输入和输出数据缓冲区的指针的指针。 此结构包含两个元素的传输数组。 第一个元素介绍包含要写入到设备的数据的缓冲区。 第二个元素描述用于保存从设备读取的数据的缓冲区。
有关如何存储控制器驱动程序实现使用 SPB_TRANSFER_LIST 结构来描述缓冲区的自定义 I/O 控制 (IOCTL) 请求的详细信息，请参阅使用自定义 Ioctl SPB_TRANSFER_LIST 结构。

### <a name="input-buffer-length"></a>输入缓冲区长度
SPB_TRANSFER_LIST 结构的大小。

### <a name="status-block"></a>状态块
如果操作成功，控制器驱动程序的状态成员设置为 STATUS_SUCCESS，并设置全双工操作期间传输的字节数 （字节读取以及写入的字节数） 的总数的信息成员。

出于各种原因，可以包含的资源不足、 无效的客户端输入和设备工作不正常情况下，此操作可能会失败。


## <a href='#ioctl-spb-lock-connection' id='ioctl-spb-lock-connection'>IOCTL_SPB_LOCK_CONNECTION 控制代码</a>

客户端 （外围设备驱动程序） 使用 IOCTL_SPB_LOCK_CONNECTION 控制代码获取与另一个客户端共享的存储连接的目标设备上的连接锁。 在连接锁保留客户端，此客户端可以独占访问设备。
系统提供 CTL_CODE 宏，这定义 I/O 控制代码中所述，用于定义 IOCTL_SPB_LOCK_CONNECTION，如下所示。

IOCTL_SPB_LOCK_CONNECTION 和 IOCTL_SPB_UNLOCK_CONNECTION 请求获取和释放附加到一个简单的外围总线的目标设备上的连接锁。 大多数客户端不使用这些输入/输出控制请求。 这些请求使用只有两个客户端共享相同的目标设备的访问权限。 有关详细信息，请参阅存储连接锁定。

两个客户端可以打开单独的逻辑连接到同一目标设备，并使用连接锁时或者客户端需要独占访问设备。 当一台客户端持有锁时，直到第一个客户端释放锁自动延迟对设备从第二个客户端的 I/O 请求。

在目标设备上的连接锁和存储控制器上的控制器锁，可以同时包含客户端。 IOCTL_SPB_LOCK_CONTROLLER 和 IOCTL_SPB_UNLOCK_CONTROLLER 请求获取和释放控制器锁。 客户端必须获取控制器锁之前获取连接锁，必须释放连接锁之前释放控制器锁。 客户端使用的控制器锁来执行总线传输 （读取和写入操作） 的有序的集作为单一的原子总线操作。 有关详细信息，请参阅 I/O 传输序列。

如果 IRP_MJ_CLEANUP 请求发送到目标设备在设备上锁定连接时，会自动终止连接锁。 清除请求发送到的目标设备时在客户端关闭其文件句柄到设备。

### <a name="status-block"></a>状态块
如果操作成功，状态成员设置为 STATUS_SUCCESS。

如果操作失败，状态成员设置为相应的错误状态代码。

如果客户端已在目标设备上保留连接锁或存储控制器，此操作的控制器锁定失败并显示状态 = STATUS_INVALID_DEVICE_REQUEST。 出于其他原因，可以包含的资源不足、 无效的客户端输入和设备工作不正常情况下，此操作可能会失败。

## <a href='#ioctl-spb-lock-controller' id='ioctl-spb-lock-controller'>IOCTL_SPB_LOCK_CONTROLLER 控制代码</a>

客户端 （外围设备驱动程序） 使用 IOCTL_SPB_LOCK_CONTROLLER 控制代码锁定存储控制器。 虽然控制器处于锁定状态，客户端具有独占使用总线访问指定的目标设备的锁。
系统提供 CTL_CODE 宏，这定义 I/O 控制代码中所述，用于定义 IOCTL_SPB_LOCK_CONTROLLER，如下所示。

若要获取的访问的目标设备的总线独占使用，客户端 （外围设备驱动程序） 将此 IOCTL 发送到目标的文件对象中。 此 IOCTL 完成后，控制器处于锁定状态，并在总线上的所有 I/O 传输 （读取或写入） 都访问指定的目标。 之间传输，控制器保持所选目标设备，但会停止时钟。

在控制器保持锁定状态，直到客户端发送 IOCTL_SPB_UNLOCK_CONTROLLER 请求以解锁控制器。 传输到或从目标设备的客户端的序列完成后，客户端必须解除对控制器，以便在控制器可以处理其他目标总线上的 I/O 请求。

如果 IRP_MJ_CLEANUP 请求发送到目标设备控制器锁定在目标上时，会自动终止锁。 清除请求发送到目标时在客户端关闭其句柄到目标。

存储控制器不需要支持 IOCTL_SPB_LOCK_CONTROLLER 和 IOCTL_SPB_UNLOCK_CONTROLLER 请求和外围设备驱动程序不应假定支持它们。

如果存储控制器驱动程序注册 EvtSpbControllerLock 回调函数，则存储 framework 扩展 (SpbCx) 将调用此函数可将 IOCTL_SPB_LOCK_CONTROLLER 请求传递给处理的存储控制器驱动程序。


### <a name="status-block"></a>状态块
如果操作成功，状态成员设置为 STATUS_SUCCESS。
此 IOCTL 可以返回多个原因，包括失败，若要配置控制器在独占访问模式下操作的错误状态。 在此模式下，控制器会保留选择，以便它是独占的总线上的所有 I/O 传输目标的目标设备。 控制器仍保持在此模式下，直到解锁。

## <a href='#ioctl-spb-unlock-connection' id='#ioctl-spb-unlock-connection'>IOCTL_SPB_UNLOCK_CONNECTION 控制代码</a>

客户端 （外围设备驱动程序） 使用 IOCTL_SPB_UNLOCK_CONNECTION I/O 控制代码来释放与另一个客户端共享的存储连接的目标设备上的连接锁。 客户端先前所发送的 IOCTL_SPB_LOCK_CONNECTION 请求以独占方式访问设备。

IOCTL_SPB_LOCK_CONNECTION 和 IOCTL_SPB_UNLOCK_CONNECTION 请求获取和释放附加到一个简单的外围总线的目标设备上的连接锁。 大多数客户端不使用这些输入/输出控制请求。 这些请求使用只有两个客户端共享相同的目标设备的访问权限。 有关详细信息，请参阅存储连接锁定。

客户端 （外围设备驱动程序） 将 IOCTL_SPB_LOCK_CONNECTION 请求发送到总线上的目标设备并且该请求已成功完成后，连接保持锁定状态，直到客户端发送 IOCTL_SPB_UNLOCK_CONNECTION 请求以解锁连接。

客户端发送 IOCTL_SPB_UNLOCK_CONNECTION 请求以释放连接锁到目标设备，当客户端不再需要独占访问设备。 该连接必须解锁，以便其他客户端可以访问该设备。

### <a name="status-block"></a>状态块
如果操作成功，状态成员设置为 STATUS_SUCCESS。

如果操作失败，状态成员设置为相应的错误状态代码。 如果客户端不保持目标设备的连接锁定，或者如果客户端仍保留在存储控制器的连接锁，此操作将失败，状态 = STATUS_INVALID_DEVICE_REQUEST。 出于其他原因，可以包含的资源不足、 无效的客户端输入和设备工作不正常情况下，此操作可能会失败。

## <a href='#ioctl-spb-unlock-controller' id='#ioctl-spb-unlock-controller'>IOCTL_SPB_UNLOCK_CONTROLLER 控制代码</a>

客户端 （外围设备驱动程序） 用 IOCTL_SPB_UNLOCK_CONTROLLER I/O 控制代码来解锁存储控制器。 客户端在之前锁定以获得独占使用的总线访问总线上的目标设备的控制器。

客户端 （外围设备驱动程序） 将 IOCTL_SPB_LOCK_CONTROLLER I/O 控制请求发送到总线上的目标设备后，控制器保持锁定状态，直到客户端发送 IOCTL_SPB_UNLOCK_CONTROLLER I/O 控制请求以解锁控制器。 客户端将这些输入/输出控制请求发送到目标设备的文件对象。

客户端发送 IOCTL_SPB_UNLOCK_CONTROLLER 请求时它已完成的传输总线上的序列，并想要发布的目标设备。 控制器必须解锁，以便它可以处理其他目标总线上的 I/O 请求。

存储控制器不需要支持 IOCTL_SPB_LOCK_CONTROLLER 和 IOCTL_SPB_UNLOCK_CONTROLLER 请求和外围设备驱动程序不应假定支持它们。

存储框架扩展 (SpbCx) 调用的存储控制器驱动程序的可选的 EvtSpbControllerUnlock 回调函数来将 IOCTL_SPB_LOCK_CONTROLLER 请求传递给处理的存储控制器驱动程序。

## <a name="status-block"></a>状态块
如果操作成功，状态成员设置为 STATUS_SUCCESS。
仅当不具有对指定的目标进行独占访问锁定的控制器客户端发送，此 IOCTL 可能会失败。


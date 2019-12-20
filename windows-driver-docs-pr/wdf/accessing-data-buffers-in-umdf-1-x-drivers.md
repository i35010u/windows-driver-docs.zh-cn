---
title: 访问 UMDF 1.x 驱动程序中的数据缓冲区
description: 访问 UMDF 1.x 驱动程序中的数据缓冲区
ms.assetid: cbd67ada-696e-403e-9b35-d8ed06a844d5
keywords:
- 数据缓冲区 WDK UMDF
- 缓冲 WDK UMDF
- 请求处理 WDK UMDF，数据缓冲区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddadcaa1e564a7399cbd58ab6180ead3e620c393
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210071"
---
# <a name="accessing-data-buffers-in-umdf-1x-drivers"></a>访问 UMDF 1.x 驱动程序中的数据缓冲区


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

当驱动程序接收到读取、写入或设备 i/o 控制请求时，请求对象将同时包含输入缓冲区或输出缓冲区。 （几个设备 i/o 控制请求提供两个输入/输出缓冲区。）

输入缓冲区包含驱动程序所需的信息。 对于写入请求，通常情况下，此信息是函数驱动程序必须发送到设备的数据。 对于设备 i/o 控制请求，输入缓冲区可能包含表明驱动程序必须执行的操作类型的信息。

输出缓冲区从驱动程序接收信息。 对于读取请求，通常情况下，此信息是函数驱动程序从设备接收的数据。 对于设备 i/o 控制请求，输出缓冲区可能接收指定的请求的 i/o 控制代码的状态或其他信息。

驱动程序用于访问请求的数据缓冲区的方法可能取决于用于访问设备数据缓冲区的驱动程序的方法。 UMDF 支持以下缓冲区访问方法：

-   版本1.9 之前的 UMDF 版本仅支持[缓冲 i/o](#using-buffered-i-o-in-umdf-drivers)访问方法。 使用这些版本的 UMDF 运行的基于 UMDF 的驱动程序只能对所有读取、写入和设备 i/o 控制请求使用缓冲 i/o 方法。 若要访问 i/o 请求的数据缓冲区，基于 UMDF 的驱动程序必须使用[**IWDFIoRequest：： GetInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getinputmemory)和[**IWDFIoRequest：： GetOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getoutputmemory)对象方法。

-   从 UMDF 版本1.9 开始，有两种访问方法：[缓冲 i/o](#using-buffered-i-o-in-umdf-drivers)和[直接 i/o](#using-direct-i-o-in-umdf-drivers)，可用于基于 UMDF 的驱动程序。 为 UMDF 版本1.9 及更高版本编写的 UMDF 驱动程序应使用[**IWDFIoRequest2：： RetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveinputbuffer)、 [**IWDFIoRequest2：： RetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveinputmemory)、 [**IWDFIoRequest2：： RetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveoutputbuffer)或[**IWDFIoRequest2：： RetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveoutputmemory)对象方法来访问数据缓冲区。

第三种访问方法（既称[缓冲还是直接 i/o](#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)）对基于 umdf 的驱动程序不可用，但 umdf 可以将从 "两者都" 方法到的 i/o 请求转换为 umdf 版本支持的方法。

在大多数情况下，基于 UMDF 的驱动程序调用相同的 UMDF 对象方法来访问数据缓冲区，无论 UMDF 和驱动程序使用的是缓冲 i/o 还是直接 i/o。 直接 i/o 通常提供比缓冲区 i/o 提供的更好的性能。

本主题中的以下部分介绍：

-   如何指定首选的[缓冲区访问方法](#specifying-a-preferred-buffer-access-method)和[首选的缓冲区检索模式](#specifying-a-buffer-retrieval-mode)

-   UMDF 如何[选择](#how-umdf-chooses-a-buffer-access-method-for-an-i-o-request)要使用的缓冲区方法和检索模式

-   驱动程序如何[获取](#how-a-driver-can-obtain-the-access-method-for-an-i-o-request)UMDF 正在使用的缓冲区访问方法

-   使用[缓冲](#using-buffered-i-o-in-umdf-drivers)的、[直接](#using-direct-i-o-in-umdf-drivers)的，并且不使用[缓冲和直接](#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)的缓冲访问方法的准则

### <a href="" id="specifying-a-preferred-buffer-access-method"></a>指定首选的缓冲区访问方法

UMDF 版本1.9 及更高版本支持缓冲和直接 i/o 访问方法。 在调用[**IWDFDriver：： CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)创建设备对象之前，驱动程序可以通过调用[**IWDFDeviceInitialize2：： SetIoTypePreference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize2-setiotypepreference)来指定想要用于设备的所有读、写和设备 i/o 控制请求的访问方法。 例如，如果驱动程序只为其某个设备的读取和写入请求指定一个首选项，则该驱动程序[主机进程](umdf-driver-host-process.md)会在将读取和写入请求传递到该设备的驱动程序时使用该缓冲 i/o 方法。 如果驱动程序为直接 i/o 指定首选项，则 UMDF 可以（但可能不）使用直接 i/o。 有关 UMDF 何时使用直接 i/o 的详细信息，请参阅[Umdf 如何为 I/o 请求选择缓冲区访问方法](#how-umdf-chooses-a-buffer-access-method-for-an-i-o-request)。

对于驱动程序支持的每个设备，驱动程序可以指定缓冲 i/o 的首选项、直接 i/o 或设备的缓冲或直接 i/o。 驱动程序可以为读取和写入请求指定一种类型的访问方法，并为设备 i/o 控制请求指定另一种类型的访问方法。 如果驱动程序未指定访问方法首选项，则 UMDF 使用缓冲方法。

对于设备 i/o 控制请求，i/o 控制代码（IOCTL）指定缓冲区访问方法。 （有关 IOCTLs 如何指定访问方法的详细信息，请参阅[定义 I/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)。）但是，UMDF 使用的访问方法可能与 IOCTL 指定的访问方法不匹配。

-   在版本1.9 之前的 UMDF 版本中，UMDF 始终对所有 i/o 控制请求使用缓冲访问方法。

-   当 IOCTL 指定缓冲 i/o 时，UMDF 版本1.9 和更高版本使用缓冲 i/o 访问方法。 如果 IOCTL 指定直接 i/o，并且如果驱动程序调用[**IWDFDeviceInitialize2：： SetIoTypePreference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize2-setiotypepreference)来指示直接 i/o 的首选项，则 umdf 可能使用直接 i/o，或者它可能使用缓冲 i/o，如[UMDF 如何为 I/o 请求选择缓冲区访问方法](#how-umdf-chooses-a-buffer-access-method-for-an-i-o-request)中所述。 有关 UMDF 如何支持指定 "非缓冲 i/o 和直接 i/o" 方法的 IOCTLs 的信息，请参阅[在 UMDF 驱动程序中使用非缓冲 i/o 或直接 i/o](#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)。

### <a href="" id="specifying-a-buffer-retrieval-mode"></a>指定缓冲区检索模式

在版本1.9 之前的 UMDF 版本中，umdf 始终会使 i/o 请求的缓冲区对驱动程序可用（通过在 UMDF 收到 i/o 请求后，将缓冲区复制到[UMDF 驱动程序主机进程](umdf-driver-host-process.md)中）。 此缓冲区检索模式称为 "*立即检索*"。 如果发生失败，则 UMDF 完成具有失败状态值的 i/o 请求，但不会将 i/o 请求传递给驱动程序。

UMDF 版本1.9 及更高版本支持直接检索和*延迟检索*模式。 延迟检索模式将 i/o 请求的缓冲区推迟到驱动程序主机进程中，直到该驱动程序尝试访问该缓冲区。 如果发生故障，缓冲区访问函数会将错误状态值返回给驱动程序。

当驱动程序调用每个设备的[**IWDFDeviceInitialize2：： SetIoTypePreference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize2-setiotypepreference)时，驱动程序可以指定缓冲区检索模式。 使用以下规则：

-   如果驱动程序指定直接 i/o 访问方法，则它还必须指定延迟检索模式。 直接 i/o 仅适用于延迟的检索。

-   编写为使用 UMDF 版本1.9 和更高版本运行的所有驱动程序应为所有 i/o 请求指定延迟检索模式，无论驱动程序选择缓冲还是直接 i/o 访问方法。 延迟检索提供更好的性能，因为它不访问驱动程序不使用的缓冲区。

如果你的驱动程序未指定缓冲区检索模式，则 UMDF 将使用立即检索。

驱动程序堆栈中所有基于 UMDF 的驱动程序都必须使用相同的检索模式。 如果某些驱动程序指定了即时检索，而某些驱动程序指定了延迟检索，则 UMDF 会立即使用。

### <a href="" id="how-umdf-chooses-a-buffer-access-method-for-an-i-o-request"></a>UMDF 如何为 i/o 请求选择缓冲区访问方法

驱动程序在调用[**IWDFDeviceInitialize2：： SetIoTypePreference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize2-setiotypepreference)时指定的访问方法可能不是 UMDF 使用的方法。 UMDF 使用以下规则来确定要使用的访问方法：

-   驱动程序堆栈中所有基于 UMDF 的驱动程序都必须使用相同的方法来访问设备的缓冲区。 如果 UMDF 确定某些驱动程序倾向于设备的缓冲 i/o 或直接 i/o，而其他驱动程序只希望使用缓冲 i/o 来处理设备，则 UMDF 对所有驱动程序使用缓冲 i/o。 如果一个或多个堆栈的驱动程序只需要缓冲 i/o，而其他人只喜欢直接 i/o，则 UMDF 会将事件记录到系统事件日志中，并且不启动驱动程序堆栈。

    你的驱动程序可以调用[**IWDFDevice2：： GetDeviceStackIoTypePreference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-getdevicestackiotypepreference)来确定 UMDF 分配给设备的读/写请求和 i/o 控制请求的缓冲区访问方法。

-   在某些情况下，驱动程序会在调用**IWDFDeviceInitialize2：： SetIoTypePreference**时为直接 i/o 指定首选项，但为了获得最佳性能，UMDF 对一个或多个设备的请求使用缓冲 i/o。 例如，如果您可以将数据复制到驱动程序缓冲区的速度快于将数据映射到可直接访问的缓冲区，则该方法对小型缓冲区使用缓冲 i/o。

    （可选）可以设置 REG\_DWORD 类型的**DirectTransferThreshold**注册表值，框架使用此值来确定框架将对其使用直接 i/o 的最小缓冲区大小。 通常，不需要提供此注册表值，因为框架使用的值可提供最佳性能。 **DirectTransferThreshold**值位于设备[硬件密钥](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-registry-trees-and-keys)下的设备**参数\\WUDF**子项下。

    此框架使用以下规则根据在**DirectTransferThreshold**中提供的值确定阈值。 提供的数字假定**页\_大小**为4096，这在基于 Itanium 的系统上是有效的。

    -   如果将**DirectTransferThreshold**设置为小于或等于8192的任何值（或**\_大小**的 2 \* 页），则框架会将阈值设置为8192。 此框架对小于8192个字节的缓冲区使用缓冲 i/o，对等于或大于8192字节的缓冲区使用直接 i/o。

    -   如果将**DirectTransferThreshold**设置为大于8192的任何值，则该框架将向上舍入到**页面\_大小**的下一个精确倍数。 同样，框架对小于阈值的缓冲区使用缓冲 i/o，并对等于或大于阈值的缓冲区使用直接 i/o。

-   对于在内存页边界上开始和结束的缓冲区空间，UMDF 只使用直接 i/o。 如果缓冲区的开头或结尾不在页面边界上，则将对该部分缓冲区使用缓冲 i/o。 换句话说，对于包含多个 i/o 请求的大型数据传输，UMDF 可能会同时使用缓冲 i/o 和直接 i/o。

-   对于设备 i/o 控制请求，如果 i/o 控制代码（IOCTL）仅指定直接 i/o，并且仅当设备的所有基于 UMDF 的驱动程序都调用了**IWDFDeviceInitialize2：： SetIoTypePreference**来指定直接访问方法，则该请求仅使用直接 i/o。

无论使用哪种缓冲区访问方法，驱动程序都使用相同的一组请求对象方法来访问数据缓冲区。 因此，大多数驱动程序通常不需要知道 UMDF 是对 i/o 请求使用缓冲 i/o 还是直接 i/o。

### <a href="" id="how-a-driver-can-obtain-the-access-method-for-an-i-o-request"></a>驱动程序如何获取 i/o 请求的访问方法

在少数情况下，如果访问方法已知，则可以提高设备和驱动程序的性能。 在这种情况下，驱动程序可以调用[**IWDFIoRequest2：： GetEffectiveIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-geteffectiveiotype)来获取 i/o 请求的缓冲区访问方法。

例如，请考虑通常使用直接 i/o 的高吞吐量设备。 由于它使用的是直接 i/o，因此驱动程序必须在验证参数之前将应用程序指定的参数复制到本地驱动程序内存，以确保应用程序在验证后不会修改参数。

由于驱动程序可能偶尔接收到使用缓冲 i/o 的缓冲区，并且缓冲 i/o 缓冲区已被复制，因此，应用程序无法修改数据，并且驱动程序在验证它们之前无需复制参数。 因此，驱动程序应检查每个请求的缓冲区访问方法，以确定它是否必须先复制参数，然后才能对其进行验证。

### <a href="" id="using-buffered-i-o-in-umdf-drivers"></a>在 UMDF 驱动程序中使用缓冲 i/o

如果你的驱动程序使用缓冲 i/o，则 UMDF 行为因请求类型的不同而有所不同。 对于读取和写入请求，驱动程序主机进程将创建驱动程序可以访问的单个中间缓冲区。

对于写入请求，驱动程序主机进程在调用驱动程序堆栈之前从调用应用程序的输入缓冲区传输输入信息。 通常，驱动程序从中间缓冲区读取输入信息，并将其写入到设备。

对于读取请求，驱动程序通常会从设备读取信息，并将其存储在中间缓冲区中。 驱动程序主机进程将输出数据从中间缓冲区复制到应用程序的输出缓冲区。

但对于设备 i/o 控制请求，驱动程序主机进程将创建两个单独的缓冲区，驱动程序可以访问这些缓冲区。 请注意，这不同于 WDM 和 KMDF 驱动程序的行为，在这种情况下，使用缓冲 i/o 发出的读取、写入和设备 i/o 控制请求会导致驱动程序访问单个中间缓冲区。 在这种情况下，输出缓冲区最初不包含任何内容，驱动程序不应从该缓冲区中读取。 此外，驱动程序写入到输入缓冲区的任何数据都将被丢弃，而不会返回给调用应用程序。

有关何时选择缓冲 i/o 的指导原则，请参阅[**WDF\_设备\_IO\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi_types/ne-wudfddi_types-_wdf_device_io_type)。

UMDF 版本1.9 及更高版本可支持即时或延迟的请求缓冲区检索。 有关详细信息，请参阅[**WDF\_设备\_IO\_缓冲区\_检索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi_types/ne-wudfddi_types-_wdf_device_io_buffer_retrieval)。

使用即时缓冲区检索模式的驱动程序必须使用[**IWDFIoRequest：： GetInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getinputmemory)和[**IWDFIoRequest：： GetOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getoutputmemory)来访问缓冲区。

使用延迟缓冲区检索模式的驱动程序可以通过调用[**IWDFIoRequest2：： RetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveinputbuffer)、 [**IWDFIoRequest2：： RetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveinputmemory)、 [**IWDFIoRequest2：： RetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveoutputbuffer)或[**IWDFIoRequest2：： RetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveoutputmemory)来访问缓冲区。

### <a href="" id="using-direct-i-o-in-umdf-drivers"></a>在 UMDF 驱动程序中使用直接 i/o

如果你的驱动程序使用直接 i/o，则驱动程序主机进程将验证指定的 i/o 请求（通常为用户模式应用程序）的发起方的缓冲空间的可访问性，将缓冲区空间锁定为物理内存，然后为该驱动程序提供对缓冲区空间的直接访问。

有关何时选择直接 i/o 的指导原则，请参阅[**WDF\_设备\_IO\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi_types/ne-wudfddi_types-_wdf_device_io_type)。

你的驱动程序可以通过调用[**IWDFIoRequest2：： RetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveinputbuffer)、 [**IWDFIoRequest2：： RetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveinputmemory)、 [**IWDFIoRequest2：： RetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveoutputbuffer)或[**IWDFIoRequest2：： RetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveoutputmemory)来访问缓冲区。

### <a href="" id="using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers"></a>在 UMDF 驱动程序中不使用缓冲 i/o 和直接 i/o

缓冲区访问方法称为*非缓冲 i/o 和直接 i/o 方法*（或者，"两者都不是" 方法）允许驱动程序直接访问应用程序的请求缓冲区指针。 基于 UMDF 的驱动程序无法使用此访问方法。

但是，某些设备 i/o 控制代码（IOCTLs）的[定义](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)指定请求使用 "这两个" 方法。 或者，UMDF 可以将此类设备 i/o 控制请求的缓冲区访问方法转换为缓冲 i/o 或直接 i/o。 请使用以下步骤：

1.  在驱动程序的 INF 文件的[**Inf DDInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)中包含[UmdfMethodNeitherAction](specifying-wdf-directives-in-inf-files.md)指令。 可以设置指令的值，以指示 UMDF 应将使用 "两个" 访问方法的设备 i/o 控制请求传递给驱动程序。 （否则，UMDF 使用错误状态值完成这些 i/o 请求。）

2.  使用 UMDF 为[缓冲 i/o](#using-buffered-i-o-in-umdf-drivers)或[直接 i/o](#using-direct-i-o-in-umdf-drivers)提供的对象方法访问 i/o 请求的缓冲区。

仅当你确定 UMDF 可以将访问方法转换为缓冲 i/o 或直接 i/o 时，才应启用使用 "两个" 方法的 IOCTL 请求支持。 例如，如果 IOCTL 指定的自定义请求不遵循[I/o 控制代码的缓冲区说明](https://docs.microsoft.com/windows-hardware/drivers/kernel/buffer-descriptions-for-i-o-control-codes)中描述的缓冲区规范规则，则 UMDF 无法转换缓冲区。

 

 






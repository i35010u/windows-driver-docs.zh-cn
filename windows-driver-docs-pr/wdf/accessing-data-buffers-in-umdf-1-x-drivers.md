---
title: 访问 UMDF 1.x 驱动程序中的数据缓冲区
description: 访问 UMDF 1.x 驱动程序中的数据缓冲区
ms.assetid: cbd67ada-696e-403e-9b35-d8ed06a844d5
keywords:
- 数据缓冲 WDK UMDF
- 缓冲区 WDK UMDF
- 请求处理 WDK UMDF，数据缓冲区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42bf8b9e47b8f20bc466e4acd4149243acb65581
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519369"
---
# <a name="accessing-data-buffers-in-umdf-1x-drivers"></a>访问 UMDF 1.x 驱动程序中的数据缓冲区


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

当驱动程序收到读取、 写入或设备的 I/O 控制请求时，请求对象将包含输入的缓冲区或输出缓冲区，或两者。 （一些设备 I/O 控制请求提供两个输入、 两个输出或两个输入/输出缓冲区。）

输入的缓冲区包含驱动程序需要的信息。 通常用于写入请求，此信息是功能驱动程序必须向设备发送的数据。 对于设备 I/O 控制请求，请输入的缓冲区可能包含指示驱动程序必须执行的操作的类型的信息。

输出缓冲区接收来自驱动程序的信息。 通常为读取请求，此信息是从设备接收功能驱动程序的数据。 对于设备 I/O 控制请求的输出缓冲区可能会收到状态或其他信息将 I/O 控制代码指定的请求。

您的驱动程序使用来访问请求的数据缓冲区的技术可以依赖于驱动程序的方法来访问设备的数据缓冲区。 UMDF 支持以下的缓冲区的访问方法：

-   仅支持 UMDF 版之前的版本 1.9[缓冲 I/O](#using-buffered-i-o-in-umdf-drivers)访问方法。 运行这些版本 UMDF 基于 UMDF 驱动程序可用于所有的读取、 写入和设备 I/O 控制请求只有缓冲的 I/O 方法。 若要访问的 I/O 请求的数据缓冲区，基于 UMDF 驱动程序必须使用[ **IWDFIoRequest::GetInputMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff559100)并[ **IWDFIoRequest::GetOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff559112)对象方法。

-   从 UMDF 1.9 版开始，两个访问方法：[缓冲 I/O](#using-buffered-i-o-in-umdf-drivers)并[直接 I/O](#using-direct-i-o-in-umdf-drivers)，可供基于 UMDF 驱动程序。 编写 UMDF 版本 1.9 及更高版本的 UMDF 驱动程序应使用[ **IWDFIoRequest2::RetrieveInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff559033)， [ **IWDFIoRequest2::RetrieveInputMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff559037)， [ **IWDFIoRequest2::RetrieveOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff559041)，或者[ **IWDFIoRequest2::RetrieveOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff559046)对象方法来访问数据缓冲区。

第三个访问方法，称为[既不缓冲，也不直接 I/O](#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)，不是可用于基于 UMDF 驱动程序，但 UMDF 可以将某些 I/O 请求从"两"方法转换为 UMDF 版本支持的方法。

在大多数情况下，基于 UMDF 驱动程序调用是否 UMDF 和驱动程序使用的缓冲的 I/O 或直接 I/O 访问数据缓冲区，将相同 UMDF 对象方法。 直接 I/O 通常提供比缓冲区 I/O 提供更好的性能。

本主题以下各节说明：

-   如何指定[首选缓冲区的访问方法](#specifying-a-preferred-buffer-access-method)和[首选的缓冲区检索模式](#specifying-a-buffer-retrieval-mode)

-   如何 UMDF[选择](#how-umdf-chooses-a-buffer-access-method-for-an-i-o-request)要使用的缓冲区方法，并检索模式

-   您的驱动程序如何才能[获取](#how-a-driver-can-obtain-the-access-method-for-an-i-o-request)UMDF 正在使用的缓冲区的访问方法

-   使用准则[缓冲](#using-buffered-i-o-in-umdf-drivers)，[直接](#using-direct-i-o-in-umdf-drivers)，并[既不缓冲，也不直接](#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)缓冲访问方法

### <a href="" id="specifying-a-preferred-buffer-access-method"></a> 指定首选的缓冲区的访问方法

UMDF 版本 1.9 及更高版本支持两种缓冲和直接 I/O 访问方法。 驱动程序可以指定想要通过调用用于所有设备的读取、 写入和设备 I/O 控制请求的访问方法[ **IWDFDeviceInitialize2::SetIoTypePreference** ](https://msdn.microsoft.com/library/windows/hardware/ff556969)之前调用[ **IWDFDriver::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff558899)创建设备对象。 例如，如果驱动程序指定的首选项则只有缓冲的 I/O 方法为将读取和写入一个其设备的请求[UMDF 驱动程序主机进程](umdf-driver-host-process.md)使用缓冲的 I/O 方法时它提供了读取和写入到的请求设备的驱动程序。 如果驱动程序指定直接 I/O 的首选项，UMDF 可以 （但可能不会） 使用直接 I/O。 有关当 UMDF 使用直接 I/O 的详细信息，请参阅[UMDF 如何选择 I/O 请求的缓冲区的访问方法](#how-umdf-chooses-a-buffer-access-method-for-an-i-o-request)。

驱动程序支持的每台设备，该驱动程序可以指定一个首选项，缓冲的 I/O、 直接 I/O，或其中任何缓冲或设备的直接 I/O。 该驱动程序可以指定一种类型的访问方法进行读取和写入请求和设备 I/O 控制请求的访问方法的另一种类型。 如果该驱动程序未指定访问方法首选项，UMDF 使用缓冲的方法。

对于设备 I/O 控制请求，I/O 控制代码 (IOCTL) 指定的缓冲区的访问方法。 (有关如何 Ioctl 指定访问方法的详细信息，请参阅[定义的 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff543023)。)但是，UMDF 使用的访问方法可能不匹配 IOCTL 指定的访问方法。

-   在 UMDF 1.9 版之前的版本，UMDF 始终将缓冲的访问方法用于所有的 I/O 控制请求。

-   如果 IOCTL 指定缓冲的 I/O，UMDF 版本 1.9 及更高版本使用缓冲的 I/O 访问方法。 如果 IOCTL 指定直接 I/O 和驱动程序调用[ **IWDFDeviceInitialize2::SetIoTypePreference** ](https://msdn.microsoft.com/library/windows/hardware/ff556969)以指示直接 I/O，UMDF 的首选项可能会使用直接 I/O 或它可能会使用缓冲I/O，如中所述[UMDF 如何选择 I/O 请求的缓冲区的访问方法](#how-umdf-chooses-a-buffer-access-method-for-an-i-o-request)。 有关如何 UMDF 支持 Ioctl 指定"既不缓冲的 I/O 也不直接 I/O"方法的信息，请参阅[使用既不缓冲 I/O，也不在 UMDF 驱动程序的直接 I/O](#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)。

### <a href="" id="specifying-a-buffer-retrieval-mode"></a> 指定缓冲区检索模式

在 UMDF 1.9 版之前的版本，UMDF 始终使 I/O 请求的缓冲区可供该驱动程序 (通过将复制到缓冲区[UMDF 驱动程序主机进程](umdf-driver-host-process.md)) 只要 UMDF 接收的 I/O 请求。 此缓冲区检索模式称为*立即检索*。 如果发生故障，UMDF 完成 I/O 请求的失败状态的值并不向驱动程序传递的 I/O 请求。

UMDF 版本 1.9 及更高版本支持这两个立即检索并*延迟检索*模式。 延迟的检索模式推迟将 I/O 请求的缓冲区复制到驱动程序主机进程，直到驱动程序将尝试访问缓冲区。 如果发生故障，缓冲区访问函数向驱动程序返回错误状态值。

您的驱动程序可以调用时指定缓冲区检索模式[ **IWDFDeviceInitialize2::SetIoTypePreference** ](https://msdn.microsoft.com/library/windows/hardware/ff556969)为每个设备。 使用以下规则：

-   如果您的驱动程序指定它还必须指定延迟的检索模式的直接 I/O 访问方法。 直接 I/O 仅适用于延迟检索。

-   所有驱动程序的编写与 UMDF 版本 1.9 运行和更高版本应延迟的检索为指定模式的所有 I/O 请求，该驱动程序选择缓冲或直接 I/O 是否访问方法。 延迟的检索提供更好的性能，因为它不会访问该驱动程序不使用的缓冲区。

如果您的驱动程序未指定缓冲检索模式，UMDF 使用立即检索。

驱动程序堆栈中的所有基于 UMDF 驱动程序必须使用相同的检索模式。 如果某些驱动程序指定立即检索，某些指定延迟的检索 UMDF 使用立即检索。

### <a href="" id="how-umdf-chooses-a-buffer-access-method-for-an-i-o-request"></a> UMDF 如何选择 I/O 请求的缓冲区的访问方法

当调用一个驱动程序指定的访问方法[ **IWDFDeviceInitialize2::SetIoTypePreference**](https://msdn.microsoft.com/library/windows/hardware/ff556969)，可能不是使用 UMDF。 UMDF 使用以下规则来确定哪个访问要使用的方法：

-   驱动程序堆栈中的所有基于 UMDF 驱动程序必须使用相同的方法，用于访问设备的缓冲区。 如果 UMDF 确定某些驱动程序首选缓冲的 I/O 或设备的直接 I/O 而其他驱动程序更希望使用仅缓冲的 I/O 设备，UMDF 使用缓冲的 I/O 的所有驱动程序。 如果一个或多个堆栈的驱动程序更喜欢缓冲的 I/O，而其他用户首选仅直接 I/O，UMDF 将事件记录到系统事件日志，并且不会启动驱动程序堆栈。

    您的驱动程序可以调用[ **IWDFDevice2::GetDeviceStackIoTypePreference** ](https://msdn.microsoft.com/library/windows/hardware/ff556934)若要确定 UMDF 已分配给设备的读/写的缓冲区访问方法请求和 I/O 控制请求。

-   在某些情况下，驱动程序指定直接 I/O 的首选项，当它调用**IWDFDeviceInitialize2::SetIoTypePreference**，但为了获得最佳性能，UMDF 使用缓冲的 I/O 的一个或多个设备的请求。 例如，UMDF 使用缓冲的 I/O 小缓冲区如果它可以将数据复制到驱动程序的缓冲区不是它可以映射用于直接访问缓冲区更快。

    或者，可以设置 REG\_DWORD 类型化**DirectTransferThreshold** framework 用来确定该框架将使用直接 I/O 的最小缓冲区大小的注册表值。 通常情况下，不需要提供此注册表值，因为框架将使用一个值，可提供最佳性能。 **DirectTransferThreshold**设备的下找到值**设备参数\\WUDF**子项，这是设备的下[硬件密钥](https://msdn.microsoft.com/library/windows/hardware/ff549538)。

    框架将使用以下规则确定基于您在中提供的值的阈值**DirectTransferThreshold**。 提供的数字假定**页上\_大小**4096，除了在基于 Itanium 的系统有效。

    -   如果您设置**DirectTransferThreshold**为任何值小于或等于为 8192 (或 2 \* **页\_大小**)，框架将阈值设置为 8192。 框架将针对等于或大于 8192 字节的缓冲区使用缓冲的 I/O 的缓冲区小于 8192 个字节，并直接 I/O。

    -   如果您设置**DirectTransferThreshold**为任何值大于 8192，框架将向上舍入到的下一步的精确倍数**页面\_大小**。 同样，框架将使用缓冲的 I/O 的缓冲区小于阈值，并直接 I/O 的缓冲区等于或大于阈值。

-   UMDF 仅使用缓冲区空间的开始和结束的内存页边界上直接 I/O。 如果开始或缓冲区的末尾不位于页边界，UMDF 使用缓冲的 I/O 缓冲区的该部分。 换而言之，UMDF 可能包含多个 I/O 请求的大型数据传输使用缓冲的 I/O 和直接 I/O。

-   对于设备 I/O 控制请求，UMDF 使用直接 I/O，I/O 控制代码 (IOCTL) 指定直接 I/O，并且仅当所有设备的基于 UMDF 的驱动程序已调用时，才**IWDFDeviceInitialize2::SetIoTypePreference**指定直接访问方法中。

驱动程序使用一组相同的请求对象方法来访问数据缓冲区，无论哪种缓冲区的访问方法。 因此，大多数驱动程序通常不需要知道是否 UMDF 使用缓冲的 I/O 或直接 I/O 的 I/O 请求。

### <a href="" id="how-a-driver-can-obtain-the-access-method-for-an-i-o-request"></a> 如何将驱动程序可以获取访问方法，I/O 请求

在少数情况下，可以提高在设备和驱动程序的性能如果已知的访问方法。 在这种情况下，您的驱动程序可以调用[ **IWDFIoRequest2::GetEffectiveIoType** ](https://msdn.microsoft.com/library/windows/hardware/ff558994)若要获取的 I/O 请求的缓冲区的访问方法。

例如，考虑高吞吐量设备，它通常使用直接 I/O。 因为它使用直接 I/O，该驱动程序必须将应用程序指定参数到本地驱动程序内存之前验证参数，以确保应用程序在验证之后不会修改参数。

由于该驱动程序可能偶尔会接收缓冲区的使用缓冲的 I/O 和缓冲的 I/O 缓冲区已复制，因为该应用程序不能修改的数据和驱动程序不需要验证它们之前复制参数。 因此，该驱动程序应检查每个请求的缓冲区的访问方法，以确定它必须验证它们之前复制参数。

### <a href="" id="using-buffered-i-o-in-umdf-drivers"></a> 在 UMDF 驱动程序中使用缓冲的 I/O

如果您的驱动程序使用缓冲的 I/O，UMDF 行为与不同，具体取决于请求的类型。 对于读取和写入请求时，驱动程序主机进程将创建一个中间缓冲区可以访问该驱动程序。

对于写请求，驱动程序主机进程将传输输入的信息从调用应用程序的输入缓冲区之前调用驱动程序堆栈。 驱动程序通常从中间缓冲区中读取输入的信息，并将其写入到设备。

对于读取请求，驱动程序通常从设备中读取信息并将其存储在中间的缓冲区中。 驱动程序主机进程将输出数据从中间缓冲区复制到应用程序的输出缓冲区。

但是，对于设备 I/O 控制请求，驱动程序主机进程创建驱动程序可访问的两个单独缓冲区。 请注意，这不同于 WDM 和 KMDF 驱动程序，针对的读取、 写入和设备使用发送的 I/O 控制请求已缓冲的 I/O 结果驱动程序访问单一、 中间缓冲区中的行为。 在这种情况下，输出缓冲区最初不包含任何内容，并驱动程序不应从其读取。 此外，驱动程序将写入到输入缓冲区的任何数据是被丢弃，并且不会返回到调用应用程序。

有关何时选择指南缓冲 I/O，请参阅[ **WDF\_设备\_IO\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff561404)。

UMDF 版本 1.9 及更高版本可支持立即或延迟检索请求的缓冲区。 有关详细信息，请参阅[ **WDF\_设备\_IO\_缓冲区\_检索**](https://msdn.microsoft.com/library/windows/hardware/ff561399)。

使用即时缓冲检索模式的驱动程序必须使用[ **IWDFIoRequest::GetInputMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff559100)并[ **IWDFIoRequest::GetOutputMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff559112)来访问缓冲区。

使用延迟的缓冲区检索模式的驱动程序可以通过调用访问缓冲区[ **IWDFIoRequest2::RetrieveInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff559033)， [ **IWDFIoRequest2::RetrieveInputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff559037)， [ **IWDFIoRequest2::RetrieveOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff559041)，或者[ **IWDFIoRequest2::RetrieveOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff559046)。

### <a href="" id="using-direct-i-o-in-umdf-drivers"></a> 在 UMDF 驱动程序中使用直接 I/O

如果您的驱动程序使用的直接 I/O，驱动程序主机进程将验证发信方的 I/O 请求 （通常在用户模式应用程序） 指定，到物理内存中，将锁定缓冲区空间，然后即可提供驱动程序的缓冲区空间的可访问性缓冲区空间的直接访问。

有关何时选择指南直接 I/O，请参阅[ **WDF\_设备\_IO\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff561404)。

您的驱动程序可以通过调用访问缓冲区[ **IWDFIoRequest2::RetrieveInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff559033)， [ **IWDFIoRequest2::RetrieveInputMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff559037)， [ **IWDFIoRequest2::RetrieveOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff559041)，或[ **IWDFIoRequest2::RetrieveOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff559046)。

### <a href="" id="using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers"></a> 使用既不缓冲 I/O，也不直接 I/O 在 UMDF 驱动程序

名为的缓冲区的访问方法*既不缓冲 I/O，也不直接 I/O 方法*（或者，"方法都不"，简称） 允许直接访问应用程序的请求缓冲区指针的驱动程序。 基于 UMDF 驱动程序不能使用这种访问方法。

但是，[定义](https://msdn.microsoft.com/library/windows/hardware/ff543023)的一些设备 I/O 控制 (Ioctl) 代码指定请求使用"不"方法。 （可选） UMDF 可以将此类设备 I/O 控制请求的缓冲区的访问方法转换为缓冲 I/O 或直接 I/O。 请使用以下步骤：

1.  包括[UmdfMethodNeitherAction](specifying-wdf-directives-in-inf-files.md)指令[ **INF DDInstall 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)的驱动程序的 INF 文件。 可以设置的指令的值，以指示 UMDF 应传递设备 I/O 控制请求使用该驱动程序的"不"访问方法。 （否则，UMDF 完成这些 I/O 请求并显示错误状态的值。）

2.  通过使用 UMDF 提供的对象方法访问 I/O 请求的缓冲区[缓冲 I/O](#using-buffered-i-o-in-umdf-drivers)或[直接 I/O](#using-direct-i-o-in-umdf-drivers)。

应启用对使用"不"方法，仅当你确信 UMDF，可以将访问方法转换为缓冲的 I/O 或直接 I/O 的 IOCTL 请求的支持。 例如，如果 IOCTL 指定自定义的请求未遵循规则，请参阅缓冲区规范[I/O 控制代码的缓冲区说明](https://msdn.microsoft.com/library/windows/hardware/ff540663)，UMDF 不能转换缓冲区。

 

 






---
title: 管理 UMDF 驱动程序中的缓冲区访问方法
description: 如果你正在编写一个 UMDF 驱动程序，则可以为框架用于读取和写入请求的缓冲区访问方法以及设备 i/o 控制请求指定首选项。
ms.assetid: BDB78BCD-1964-431B-BE99-CABA6DF44D7A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac48e52baff48165c5a02741ce034308f25ca774
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843153"
---
# <a name="managing-buffer-access-methods-in-umdf-drivers"></a>管理 UMDF 驱动程序中的缓冲区访问方法


如果你正在编写一个 UMDF 驱动程序，则可以为框架用于读取和写入请求的[缓冲区访问方法](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)以及设备 i/o 控制请求指定*首选项*。 UMDF 驱动程序提供的值仅为首选项，不保证框架使用这些值。

-   [指定首选的缓冲区访问方法](#specifying-preferred-buffer-access-method)
-   [检索 i/o 请求的访问方法](#retrieving-access-method)
-   [不从缓冲 i/o 或直接 i/o 转换](#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)

## <a href="" id="specifying-preferred-buffer-access-method"></a>指定首选的缓冲区访问方法


从 UMDF 版本2.0 开始，UMDF 驱动程序会调用[**WdfDeviceInitSetIoTypeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)来注册读/写请求和设备 i/o 控制请求的首选访问方法。

如果驱动程序未调用[**WdfDeviceInitSetIoTypeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)，则 UMDF 会将对此设备的 i/o 请求使用缓冲方法。

框架使用以下规则来确定要使用的访问方法：

-   驱动程序堆栈中的所有 UMDF 驱动程序都必须使用相同的方法来访问设备的缓冲区，并且该框架提供了缓冲 i/o 的首选项。

    如果 UMDF 确定某些驱动程序倾向于设备的缓冲 i/o 或直接 i/o，而其他驱动程序只希望使用缓冲 i/o 来处理设备，则 UMDF 对所有驱动程序使用缓冲 i/o。 如果一个或多个堆栈的驱动程序只需要缓冲 i/o，而其他人只喜欢直接 i/o，则 UMDF 会将事件记录到系统事件日志中，并且不启动驱动程序堆栈。

    驱动程序可以调用[**WdfDeviceGetDeviceStackIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetdevicestackiotype)来确定 UMDF 分配给设备的读/写请求和 i/o 控制请求的缓冲区访问方法。

-   在某些情况下，UMDF 将直接 i/o 分配给设备，但为了获得最佳性能，请对一个或多个设备的请求使用缓冲 i/o。 例如，如果您可以将数据复制到驱动程序缓冲区的速度快于将数据映射到可直接访问的缓冲区，则该方法对小型缓冲区使用缓冲 i/o。

    或者，驱动程序在调用[**WdfDeviceInitSetIoTypeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)时可以提供**DirectTransferThreshold**值。 框架使用此值来确定框架将对其使用直接 i/o 的最小缓冲区大小。 通常，您不需要提供此值，因为框架使用提供最佳性能的设置。

-   对于在内存页边界上开始和结束的缓冲区空间，UMDF 只使用直接 i/o。 如果缓冲区的开头或结尾不在页面边界上，则将对该部分缓冲区使用缓冲 i/o。 换句话说，对于包含多个 i/o 请求的大型数据传输，UMDF 可能会同时使用缓冲 i/o 和直接 i/o。

-   对于设备 i/o 控制请求，如果 i/o 控制代码（IOCTL）仅指定直接 i/o，并且该设备的所有 UMDF 驱动程序都已调用[**WdfDeviceInitSetIoTypeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)来指定直接访问方法，则该设备仅使用直接 i/o。

## <a href="" id="retrieving-access-method"></a>检索 i/o 请求的访问方法


无论使用哪种缓冲区访问方法，驱动程序都使用相同的一组请求对象方法来访问数据缓冲区。 因此，大多数驱动程序通常不需要知道 UMDF 是对 i/o 请求使用缓冲 i/o 还是直接 i/o。

在某些情况下，如果知道 i/o 请求的访问方法，则可以改善驱动程序的性能。 例如，请考虑通常使用直接 i/o 的高吞吐量设备。 当驱动程序收到 i/o 请求时，它会将数据从共享缓冲区空间复制到本地驱动程序内存中进行验证。

但是，驱动程序可能偶尔接收到使用缓冲 i/o 的缓冲区。 由于 i/o 管理器已经将这些数据复制到中间缓冲区，因此该驱动程序不需要在本地复制参数。 通过避免复制操作，驱动程序可提高性能。

UMDF 驱动程序调用[**WdfRequestGetEffectiveIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgeteffectiveiotype)来获取 i/o 请求的缓冲区访问方法。 如上所述，特定请求的 i/o 类型可能与用于设备的框架分配的 i/o 类型设置不同。

## <a href="" id="using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers"></a>不从缓冲 i/o 或直接 i/o 转换


UMDF 驱动程序无法使用 "这两个" 方法。

但是，某些设备 i/o 控制代码（IOCTLs）的[定义](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)指定请求使用 "这两个" 方法。 或者，UMDF 驱动程序可以将此类设备 i/o 控制请求的缓冲区访问方法转换为缓冲 i/o 或直接 i/o。 请使用以下步骤：

1.  在驱动程序的 INF 文件的[**Inf DDInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)中包含[UmdfMethodNeitherAction](specifying-wdf-directives-in-inf-files.md)指令。 可以设置指令的值，以指示 UMDF 应将使用 "两个" 访问方法的设备 i/o 控制请求传递给驱动程序。 （否则，UMDF 使用错误状态值完成这些 i/o 请求。）

2.  使用 UMDF 为[缓冲 i/o](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers#buffered)或[直接 i/o](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers#direct)提供的对象方法访问 i/o 请求的缓冲区。

仅当你确定 UMDF 可以将访问方法转换为缓冲 i/o 或直接 i/o 时，才应启用使用 "两个" 方法的 IOCTL 请求支持。 例如，如果 IOCTL 指定的自定义请求不遵循[I/o 控制代码的缓冲区说明](https://docs.microsoft.com/windows-hardware/drivers/kernel/buffer-descriptions-for-i-o-control-codes)中描述的缓冲区规范规则，则 UMDF 无法转换缓冲区。

 

 






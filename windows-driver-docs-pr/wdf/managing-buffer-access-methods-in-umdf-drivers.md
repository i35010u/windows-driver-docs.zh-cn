---
title: 管理 UMDF 驱动程序中的缓冲区访问方法
description: 如果你正在编写 UMDF 驱动程序，则可以指定框架使用的缓冲区的访问方法的首选项读取和写入请求，以及设备 I/O 控制请求。
ms.assetid: BDB78BCD-1964-431B-BE99-CABA6DF44D7A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d68edfeb7fad453149a1ed3ff5a07949b5394d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371743"
---
# <a name="managing-buffer-access-methods-in-umdf-drivers"></a>管理 UMDF 驱动程序中的缓冲区访问方法


如果你正在编写 UMDF 驱动程序，您可以指定*首选项*有关[缓冲访问方法](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)框架使用的读取和写入请求，以及设备 I/O 控制请求。 UMDF 驱动程序提供的值是仅首选项，并不保证由框架使用。

-   [指定首选的缓冲区的访问方法](#specifying-preferred-buffer-access-method)
-   [I/O 请求检索的访问方法](#retrieving-access-method)
-   [转换从既不缓冲 I/O，也不直接 I/O](#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)

## <a href="" id="specifying-preferred-buffer-access-method"></a>指定首选的缓冲区的访问方法


从 UMDF 2.0 版开始，UMDF 驱动程序调用[ **WdfDeviceInitSetIoTypeEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)进行注册，读/写请求的首选的访问方法和设备 I/O 控制请求。

如果该驱动程序不会调用[ **WdfDeviceInitSetIoTypeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)，UMDF 使用缓冲的方法，以便对此设备的 I/O 请求。

框架将使用以下规则确定的访问方法，以使用：

-   驱动程序堆栈中的所有 UMDF 驱动程序必须都使用相同的方法，用于访问设备的缓冲区和 framework 提供的首选项设置为缓冲的 I/O。

    如果 UMDF 确定某些驱动程序首选缓冲的 I/O 或设备的直接 I/O 而其他驱动程序更希望使用仅缓冲的 I/O 设备，UMDF 使用缓冲的 I/O 的所有驱动程序。 如果一个或多个堆栈的驱动程序更喜欢缓冲的 I/O，而其他用户首选仅直接 I/O，UMDF 将事件记录到系统事件日志，并且不会启动驱动程序堆栈。

    您的驱动程序可以调用[ **WdfDeviceGetDeviceStackIoType** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegetdevicestackiotype)若要确定 UMDF 已分配给设备的读/写的缓冲区访问方法请求和 I/O 控制请求。

-   在某些情况下，UMDF 将直接 I/O 分配到设备，但为了获得最佳性能，使用缓冲 I/O 的一个或多个设备的请求。 例如，UMDF 使用缓冲的 I/O 小缓冲区如果它可以将数据复制到驱动程序的缓冲区不是它可以映射用于直接访问缓冲区更快。

    （可选） 可以提供您的驱动程序**DirectTransferThreshold**值时，它调用[ **WdfDeviceInitSetIoTypeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)。 该框架使用此值以确定该框架将使用直接 I/O 的最小缓冲区大小。 通常情况下，不需要提供此值，因为框架使用提供最佳性能的设置。

-   UMDF 仅使用缓冲区空间的开始和结束的内存页边界上直接 I/O。 如果开始或缓冲区的末尾不位于页边界，UMDF 使用缓冲的 I/O 缓冲区的该部分。 换而言之，UMDF 可能包含多个 I/O 请求的大型数据传输使用缓冲的 I/O 和直接 I/O。

-   对于设备 I/O 控制请求，UMDF 使用直接 I/O，如果 I/O 控制代码 (IOCTL) 指定直接 I/O，并且仅当该设备的 UMDF 驱动程序的所有调用仅[ **WdfDeviceInitSetIoTypeEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)若要指定直接访问方法。

## <a href="" id="retrieving-access-method"></a>I/O 请求检索的访问方法


驱动程序使用一组相同的请求对象方法来访问数据缓冲区，无论哪种缓冲区的访问方法。 因此，大多数驱动程序通常不需要知道是否 UMDF 使用缓冲的 I/O 或直接 I/O 的 I/O 请求。

在某些情况下，如果您知道的 I/O 请求的访问方法可以提高驱动程序的性能。 例如，考虑高吞吐量设备，它通常使用直接 I/O。 当驱动程序收到的 I/O 请求时，它将数据从复制的共享的缓冲区空间到本地驱动程序内存中进行验证。

但是，该驱动程序可能会偶尔收到使用缓冲的 I/O 的缓冲区。 由于 I/O 管理器已具有到中间缓冲区复制此数据，则不需要将复制参数本地驱动程序。 通过避免复制操作，该驱动程序可以提高性能。

UMDF 驱动程序调用[ **WdfRequestGetEffectiveIoType** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgeteffectiveiotype)若要获取的 I/O 请求的缓冲区的访问方法。 如上所述，特定请求的 I/O 类型可能不同于 framework 分配 I/O 类型设置的设备。

## <a href="" id="using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers"></a> 转换从既不缓冲 I/O，也不直接 I/O


UMDF 驱动程序不能使用"不"方法。

但是，[定义](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)的一些设备 I/O 控制 (Ioctl) 代码指定请求使用"不"方法。 （可选） UMDF 驱动程序可以将此类设备 I/O 控制请求的缓冲区的访问方法转换为缓冲 I/O 或直接 I/O。 请使用以下步骤：

1.  包括[UmdfMethodNeitherAction](specifying-wdf-directives-in-inf-files.md)指令[ **INF DDInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)的驱动程序的 INF 文件。 可以设置的指令的值，以指示 UMDF 应传递设备 I/O 控制请求使用该驱动程序的"不"访问方法。 （否则，UMDF 完成这些 I/O 请求并显示错误状态的值。）

2.  通过使用 UMDF 提供的对象方法访问 I/O 请求的缓冲区[缓冲 I/O](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers#buffered)或[直接 I/O](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers#direct)。

应启用对使用"不"方法，仅当你确信 UMDF，可以将访问方法转换为缓冲的 I/O 或直接 I/O 的 IOCTL 请求的支持。 例如，如果 IOCTL 指定自定义的请求未遵循规则，请参阅缓冲区规范[I/O 控制代码的缓冲区说明](https://docs.microsoft.com/windows-hardware/drivers/kernel/buffer-descriptions-for-i-o-control-codes)，UMDF 不能转换缓冲区。

 

 






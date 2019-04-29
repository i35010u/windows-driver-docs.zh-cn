---
title: DMA 验证
description: DMA 验证
ms.assetid: ffcb718a-63f5-49ff-9d36-67b2aa59761f
keywords:
- DMA 验证功能 WDK Driver Verifier
- HAL 验证 WDK 驱动程序验证程序
- 常见缓冲区 DMA WDK Driver Verifier
- 数据包 DMA WDK Driver Verifier
- 散播-聚集 DMA WDK Driver Verifier
- 系统 DMA WDK Driver Verifier
- 直接内存访问 WDK 驱动程序验证程序
- DMA 错误 WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dc19e70147d3a8ece2a99ea6da041a01185b75c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358085"
---
# <a name="dma-verification"></a>DMA 验证


## <span id="ddk_dma_verification_tools"></span><span id="DDK_DMA_VERIFICATION_TOOLS"></span>


DMA 验证监视使用直接内存访问 (DMA)。 因为 DMA 例程已更改为已开发了 Windows，许多驱动程序进行不正确使用 DMA 调用。 此外，某些驱动程序编写人员尝试完全跳过的 HAL DMA 子系统。 这种做法可以引入该驱动程序隐蔽程序错误。

Driver Verifier DMA 验证选项尝试捕获 DMA 的常见错误。 连同 **！ dma**内核调试器扩展，可以用它来验证驱动程序以正确的方式使用 DMA。

此驱动程序验证程序选项也称为*HAL 验证*。 由驱动程序验证工具生成某些错误消息可能会使用此术语。

此驱动程序验证程序选项才可用在 Windows XP 及更高版本。

### <a name="span-iddifferenttypesofdmaspanspan-iddifferenttypesofdmaspandifferent-types-of-dma"></a><span id="different_types_of_dma"></span><span id="DIFFERENT_TYPES_OF_DMA"></span>不同类型的 DMA

DMA 是一种机制，通过该硬件设备可以传输数据，从内存而无需使用处理器。 设置在传输时，所需的处理器和完成传输时，设备将信号处理器。 此系统的优点是 DMA 传输在执行时，处理器可以执行其他任务。

有几种类型的 DMA 使用在 Windows 2000 及更高版本：

<span id="Common-buffer_DMA"></span><span id="common-buffer_dma"></span><span id="COMMON-BUFFER_DMA"></span>*常见缓冲区 DMA*  
常见缓冲区 DMA 由硬件和软件系统可以分配可访问的单个缓冲区时执行。 该驱动程序负责将同步到缓冲区的访问。 不缓存内存，使此同步更轻松的驱动程序。 设置后的常见缓冲区，该驱动程序和硬件可以直接写入中无需任何干预的缓冲区的地址从 HAL。

<span id="Packet_DMA"></span><span id="packet_dma"></span><span id="PACKET_DMA"></span>*DMA 数据包*  
DMA 数据包执行时必须使用映射的硬件的单一现有缓冲区。 使用 DMA 数据包的一个示例是文件的从内存到磁盘传输。 在此情况下使用常见缓冲区 DMA 是一种浪费，因为该文件必须在硬件无法将其传输到磁盘之前传输到常见的缓冲区。 相反，可查阅 HAL;它为驱动程序帮助查找实际的缓冲区在内存中的硬件所需的信息。 此操作十分复杂，涉及才能在不同的体系结构之间工作的例程的需要。

<span id="Scatter_gather_DMA"></span><span id="scatter_gather_dma"></span><span id="SCATTER_GATHER_DMA"></span>*散播-聚集 DMA*  
散播-聚集 DMA 是一种快捷方法，同时设置多个数据包 DMA 传输。 如果正在通过网络传输数据包，例如，网络堆栈的每个部分添加其自己的标头 （TCP、 IP、 以太网，等等）。 从内存中的不同位置都被分配这些标头。 在这种情况下，散播-聚集 DMA 可以通过将每个标头以及访问的数据段映射的硬件的 hal 发出批处理请求节省时间。 而无需调用该数据包 DMA 例程数据包的每个部分，此方法一次，调用每个例程，并可让负责映射每个单独的 HAL。

**请注意**  *散播-聚集功能*并不意味着该设备可以使用散播-聚集例程。 散播-聚集功能是指设备描述，该值指示可以读取或写入内存，而不是只为某个范围中的任意区域从设备中的标志。

 

<span id="System_DMA"></span><span id="system_dma"></span><span id="SYSTEM_DMA"></span>*系统 DMA*  
由编程主板以直接执行传输上的系统 DMA 控制器执行系统 DMA。 只有 ISA 卡可以使用系统 DMA。

### <a name="span-ideffectsofdmaverificationspanspan-ideffectsofdmaverificationspaneffects-of-dma-verification"></a><span id="effects_of_dma_verification"></span><span id="EFFECTS_OF_DMA_VERIFICATION"></span>DMA 验证的影响

DMA 验证活动后，驱动程序验证程序检测到误用了 DMA 例程中包括：

-   无限大或 underrunning DMA 内存缓冲区 （这些错误可由硬件或驱动程序）。

-   重复释放常见缓冲区、 适配器通道，映射注册，或分散/集中列表。

-   通过常见的缓冲区、 适配器通道、 地图寄存器，散播-聚集列表或适配器未在释放泄漏内存。

-   一次遇到多个适配器通道存在的适配器。

-   尝试使用已释放并不再存在的适配器。

-   不刷新适配器缓冲区。

-   具有过多的适配器的未完成的引用计数。

-   对可分页的缓冲区 （DMA 传输开始前，应锁定所有缓冲区） 执行 DMA。

-   对与重整标志 MDL 执行 DMA。

-   引用无效的系统地址，第一个 MDL 之前, 或之后的第一个 MDL，末尾，或使用的长度超过 MDL 缓冲区并跨越页边界内 MDL 的传输长度。

-   一次分配过多的映射寄存器或分配多个映射寄存器比允许的最大数目。

-   双映射映射的注册。

-   尝试释放映射寄存器，而某些仍然映射。

-   尝试刷新未映射的映射寄存器。

-   尝试刷新映射注册文件末尾的字节太多。

-   在不正确的 IRQL 调用 DMA 例程。

-   传递 null 值 DMA\_HAL 例程的适配器。

-   将传递一个地址和 MDL 给 HAL 例程的地址不包含在 MDL 时。

-   正在尝试映射已映射的地址范围。

-   尝试刷新未映射的缓冲区。

-   正在尝试映射传输的长度为零的缓冲区。

-   调用已过时的函数[ **HalGetAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff546596) (所有驱动程序必须使用[ **IoGetDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff549220)相反)。

驱动程序验证工具监视驱动程序的行为，并发出错误检查 0xE6，如果出现任何这些冲突。 请参阅[ **Bug 检查 0xE6** ](https://msdn.microsoft.com/library/windows/hardware/ff560341) (驱动程序\_VERIFIER\_DMA\_冲突) 的 bug 列表检查参数。

### <a name="span-idwhenisdmaverificationusefulspanspan-idwhenisdmaverificationusefulspanwhen-is-dma-verification-useful"></a><span id="when_is_dma_verification_useful_"></span><span id="WHEN_IS_DMA_VERIFICATION_USEFUL_"></span>何时适合 DMA 验证？

使用 DMA 直接 （通过调用 HAL DMA 例程） 的所有驱动程序应使用 DMA 验证测试。

此外，微型端口驱动程序应还进行测试，因为它们通常使用 DMA 间接 （通过调用使用 DMA 端口驱动程序）。

DMA 验证还可以检测内存损坏情况，因为它可以找出时任一驱动程序或硬件设备就会发生溢出 DMA 缓冲区的有效方法。

### <a name="span-idmonitoringdmaverificationspanspan-idmonitoringdmaverificationspanmonitoring-dma-verification"></a><span id="monitoring_dma_verification"></span><span id="MONITORING_DMA_VERIFICATION"></span>监视 DMA 验证

内核调试器扩展 **！ dma**可以用于显示大量 DMA 信息。 它可以显示有关每个 DMA 适配器的行为的各种详细信息。 没有的详细的示例 **！ dma**扩展，以及有关调试器扩展，文档中的 Windows 调试工具软件包的常规信息。 请参阅[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)有关详细信息。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

可以使用驱动程序验证程序管理器或 Verifier.exe 命令行来激活一个或多个驱动程序的 DMA 验证功能。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。

-   **在命令行**

    在命令行中，由表示 DMA 验证选项**位 7 (0x80)**。 若要激活 DMA 验证，使用 0x80 标志值，或将 0x80 添加到标志值。 例如：

    ```
    verifier /flags 0x80 /driver MyDriver.sys
    ```

    在下一次启动后，该功能将处于活动状态。

    在 Windows Vista 和更高版本的 Windows 上，您可以还激活和停 DMA 验证用而无需重启计算机，通过添加 **/volatile**命令参数。 例如：

    ```
    verifier /volatile /flags 0x80 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时将丢失。 有关详细信息，请参阅[使用易失性设置](using-volatile-settings.md)。

    DMA 验证功能也包含在标准设置。 例如：

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **使用驱动程序验证程序管理器**

    1.  启动驱动程序验证器管理器。 类型**Verifier**在命令提示符窗口中。
    2.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步**。
    3.  选择**从完整的列表中选择单个设置**。
    4.  选择 （选中） **DMA 验证**。

    DMA 验证功能也包含在标准设置。 若要使用此功能，驱动程序验证程序管理器中，单击**创建标准设置**。

 

 






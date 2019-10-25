---
title: DMA 验证
description: DMA 验证
ms.assetid: ffcb718a-63f5-49ff-9d36-67b2aa59761f
keywords:
- DMA 验证功能 WDK 驱动程序验证程序
- HAL 验证 WDK 驱动程序验证程序
- 常见缓冲区 DMA WDK 驱动程序验证程序
- 数据包 DMA WDK 驱动程序验证程序
- 散播-聚集 DMA WDK 驱动程序验证程序
- 系统 DMA WDK 驱动程序验证程序
- 直接内存访问 WDK 驱动程序验证程序
- DMA 错误 WDK 驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 915f749073f11e6da9b0b8d5f30fb1784765eef7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839566"
---
# <a name="dma-verification"></a>DMA 验证


## <span id="ddk_dma_verification_tools"></span><span id="DDK_DMA_VERIFICATION_TOOLS"></span>


DMA 验证监视直接内存访问（DMA）的使用情况。 由于 DMA 例程在 Windows 开发后发生了更改，因此许多驱动程序对 DMA 调用的使用不正确。 此外，某些驱动程序编写器会尝试完全绕过 HAL DMA 子系统。 这种做法可以将精确性受损 bug 引入驱动程序中。

驱动程序验证程序的 DMA 验证选项尝试捕获常见的 DMA 错误。 除了 **！ dma**内核调试器扩展，它还可用于验证驱动程序是否以正确的方式使用 dma。

此驱动程序验证程序选项也称为*HAL 验证*。 驱动程序验证程序生成的一些错误消息可能使用此术语。

此驱动程序验证程序选项仅在 Windows XP 和更高版本中可用。

### <a name="span-iddifferent_types_of_dmaspanspan-iddifferent_types_of_dmaspandifferent-types-of-dma"></a><span id="different_types_of_dma"></span><span id="DIFFERENT_TYPES_OF_DMA"></span>不同类型的 DMA

DMA 是一种机制，通过该机制，硬件设备可以在不使用处理器的情况下将数据传入或传出内存。 需要处理器来设置传输，而设备在完成传输时将发出信号通知处理器。 此系统的优点是在执行 DMA 传输过程中，处理器可以执行其他任务。

Windows 2000 和更高版本中使用了几种类型的 DMA：

<span id="Common-buffer_DMA"></span><span id="common-buffer_dma"></span><span id="COMMON-BUFFER_DMA"></span>*常见缓冲区 DMA*  
当系统可以分配可同时由硬件和软件访问的单个缓冲区时，会执行公用缓冲区 DMA。 驱动程序负责同步对缓冲区的访问。 不缓存内存，这使得驱动程序的同步更为容易。 设置公用缓冲区后，驱动程序和硬件都可以直接写入缓冲区中的地址，而无需通过 HAL 进行任何干预。

<span id="Packet_DMA"></span><span id="packet_dma"></span><span id="PACKET_DMA"></span>*数据包 DMA*  
当存在一个必须映射以便硬件使用的现有缓冲区时，将执行数据包 DMA。 使用包 DMA 的一个示例是将文件从内存传输到磁盘。 在这种情况下使用公用缓冲区 DMA 会浪费空间，因为在硬件可以将文件传输到磁盘之前，必须将该文件传输到公共缓冲区。 相反，我们会咨询 HAL;它为驱动程序提供所需的信息，以帮助硬件在内存中查找实际缓冲区。 此操作非常复杂，只需涉及到跨不同体系结构工作的例程。

<span id="Scatter_gather_DMA"></span><span id="scatter_gather_dma"></span><span id="SCATTER_GATHER_DMA"></span>*散点/集合 DMA*  
散点/集合 DMA 是一种快捷方法，可同时设置多个数据包 DMA 传输。 例如，如果要通过网络传输数据包，则网络堆栈的每个部分都会添加自己的标头（TCP、IP、以太网等）。 将从内存中的不同位置分配这些标头。 在这种情况下，散点/集合 DMA 通过向 HAL 发出批处理请求来映射每个标头和数据段以供硬件访问，从而节省时间。 此方法不需要调用每个数据包的每个部分，而是调用每个例程一次，并让 HAL 负责单独映射每个例程。

**请注意**，  *散点/收集功能*并不意味着设备可以使用散点/收集例程。 散点/收集功能是指设备说明中的一个标志，该标志指示该设备能够从内存中的任何区域读取或写入，而不只是特定范围。

 

<span id="System_DMA"></span><span id="system_dma"></span><span id="SYSTEM_DMA"></span>*系统 DMA*  
系统 DMA 通过对主板上的系统 DMA 控制器进行编程来执行直接传输。 只有 ISA 卡才能使用系统 DMA。

### <a name="span-ideffects_of_dma_verificationspanspan-ideffects_of_dma_verificationspaneffects-of-dma-verification"></a><span id="effects_of_dma_verification"></span><span id="EFFECTS_OF_DMA_VERIFICATION"></span>DMA 验证的效果

当 DMA 验证处于活动状态时，驱动程序验证器会检测到 DMA 例程的误用了，其中包括：

-   DMA 内存缓冲区的 Overrunning 或 underrunning （这些错误可以由硬件或驱动程序进行）。

-   双释放公共缓冲区、适配器通道、映射寄存器或散点/集合列表。

-   通过释放公用缓冲区、适配器通道、映射寄存器、散点/集合列表或适配器来泄漏内存。

-   一次有一个适配器有多个适配器通道。

-   尝试使用已释放但不再存在的适配器。

-   不刷新适配器缓冲区。

-   适配器的未完成引用计数太多。

-   对可分页缓冲区执行 DMA （所有缓冲区应在 DMA 传输开始前锁定）。

-   在带有损坏标志的 MDL 上执行 DMA。

-   引用无效的系统地址（在第一个 MDL 之前，或在第一个 MDL 结束之后或在第一个 MDL 结束之后），或使用比 MDL 缓冲区更长的传输长度，并在 MDL 内跨过页面边界。

-   一次分配的映射寄存器过多，或者分配的映射寄存器超过了允许的最大数量。

-   映射寄存器的双映射。

-   在某些情况下，尝试释放映射寄存器仍会被映射。

-   正在尝试刷新尚未映射的映射寄存器。

-   尝试在映射注册文件的末尾刷新太多字节。

-   以不正确的 IRQL 调用 DMA 例程。

-   将 null 值 DMA\_适配器传递到 HAL 例程。

-   当地址不包含在 MDL 中时，将地址和 MDL 传递到 HAL 例程。

-   尝试映射已映射的地址范围。

-   正在尝试刷新未映射的缓冲区。

-   正在尝试映射长度为零的缓冲区以进行传输。

-   调用过时的函数[**HalGetAdapter**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85)) （所有驱动程序都必须使用[**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter) ）。

驱动程序验证程序监视驱动程序的行为，并在发生任何这些冲突时发出 bug 检查0xE6。 有关错误检查参数的列表，请参阅[**Bug 检查 0xE6**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xe6--driver-verifier-dma-violation) （DRIVER\_VERIFIER\_DMA\_冲突）。

### <a name="span-idwhen_is_dma_verification_useful_spanspan-idwhen_is_dma_verification_useful_spanwhen-is-dma-verification-useful"></a><span id="when_is_dma_verification_useful_"></span><span id="WHEN_IS_DMA_VERIFICATION_USEFUL_"></span>DMA 验证是否有用？

直接使用 DMA 的所有驱动程序（通过调用 HAL DMA 例程）都应该使用 DMA 验证进行测试。

此外，还应测试微型端口驱动程序，因为它们经常使用 DMA （通过调用使用 DMA 的端口驱动程序）。

DMA 验证也可以是检测内存损坏的有效方法，因为当驱动程序或硬件设备溢出 DMA 缓冲区时，DMA 验证会发现。

### <a name="span-idmonitoring_dma_verificationspanspan-idmonitoring_dma_verificationspanmonitoring-dma-verification"></a><span id="monitoring_dma_verification"></span><span id="MONITORING_DMA_VERIFICATION"></span>监视 DMA 验证

内核调试器扩展 **！ dma**可用于显示大量 dma 信息。 它可以显示有关每个 DMA 适配器的行为的各种详细信息。 有关详细信息，请参阅 "适用于 Windows 的调试工具" 包中的内容，以及有关调试器**扩展的一般**信息。 有关详细信息，请参阅[Windows 调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

你可以通过使用驱动程序验证器管理器或 Verifier 命令行为一个或多个驱动程序激活 DMA 验证功能。 有关详细信息，请参阅[选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。

-   **在命令行中**

    在命令行中，DMA 验证选项由**第7位（0x80）** 表示。 若要激活 DMA 验证，请使用值为0x80 的标志值或将0x80 添加到标志值。 例如：

    ```
    verifier /flags 0x80 /driver MyDriver.sys
    ```

    此功能将在下一次启动后处于活动状态。

    在 Windows Vista 和更高版本的 Windows 上，还可以通过将 **/volatile**参数添加到命令，来激活和停用 DMA 验证，而无需重新启动计算机。 例如：

    ```
    verifier /volatile /flags 0x80 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时，此设置会丢失。 有关详细信息，请参阅[使用可变设置](using-volatile-settings.md)。

    "DMA 验证" 功能也包含在标准设置中。 例如：

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **使用驱动程序验证器管理器**

    1.  启动驱动程序验证器管理器。 在命令提示符窗口中键入**Verifier** 。
    2.  选择 "**创建自定义设置（对于代码开发人员）** "，然后单击 "**下一步**"。
    3.  选择 "**从完整列表中选择单个设置**"。
    4.  选择（检查） **DMA 验证**。

    "DMA 验证" 功能也包含在标准设置中。 若要使用此功能，请在驱动程序验证器管理器中单击 "**创建标准设置**"。

 

 






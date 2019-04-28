---
title: USB 双向扩展程序
description: 介绍了使用 Bidi XML 文件和一个名为 USB Bidi 扩展程序的 Javascript 文件的组合的 USB 设备的双向支持。
ms.assetid: C4012369-F1C6-4EBC-8DAE-F4E551DE782D
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1f265d1402c548515773528a57bb419c6dee6059
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346560"
---
# <a name="usb-bidi-extender"></a>USB 双向扩展程序


Windows 使用 Bidi XML 文件和一个名为 USB Bidi 扩展程序的 Javascript 文件的组合允许 USB 设备的制造商都支持双向通信 (Bidi)。

USB Bidi 扩展器允许应用程序中使用 Bidi USB 作为传输机制。 Javascript 实现不支持任何设备流控制，或控制的信息与打印作业在打印过程中任何多路复用。

默认情况下，Bidi 查询和状态将请求路由通过用于打印的 USB 设备接口。 这允许状态使用的完全双向通信**getSchemas** JavaScript 方法，如也为允许使用的集运算**setSchema** JavaScript 方法。 完整的双向通信是可能的而没有打印作业发送到打印设备。

在打印时，写入会被阻止该打印作业的数据，因此**getStatus**方法用于从设备中，使用仅读取的通道获取未经请求的状态。 但是，如果设备支持辅助 USB 接口，则**requestStatus**方法函数用于在打印设备的同时从打印机获取状态。

在 Windows 8.1 v4 驱动程序模型已扩展，适用于基于主机的设备提供支持。 除此之外，USBMon 进行更新，允许 Ihv 使用 JavaScript 代码，以获得更好地控制打印路径，并执行打印基于作业的操作。 提供新的 Bidi JavaScript 入口点的 Api 添加了一些更新。 这些 Api 符合 USBMon 中的现有函数。

**startPrintJob**。 此新函数与在 USBMon startDocPort 密切合作。 作为每个新的 USB 端口连接到 USBMon 将调用 IHV 提供 JavaScript，使其以执行它需要的任何作业前处理基于主机的打印设备上启动打印作业。 这可能包括在作业的属性包，查询设备的当前状态和配置数据或执行任何操作中设置作业的全局属性。 已完成的任务都完全依赖于设备和 IHV。

**writePrintData**。 此新函数与在 USBMon writePort 密切合作。 时 USBMon 的打印操作期间收到来自后台处理程序的每个 writePort 函数调用，提供的打印数据需要发送到通过 IHV JavaScript 函数基于主机的设备。 这允许 IHV JS 决定什么应发送到设备这一次。 IHV 可以删除、 添加或根据需要保存的数据缓冲区的部分。 这允许 IHV 来完全控制发送到设备的内容时。 这将帮助通过手动双面打印为这种情况下使 IHV 有机会保存消失 （在一个持久流） 的偶数页打印作业用于处理从后台处理程序收到的所有数据后的数据。 IHV 还可以使用 printerBidiSchemaResponses 对象在处理作业期间返回的打印作业状态或设备状态。

**endPrintJob**。 此新函数与在 USBMon endDocPort 密切合作。 当 USBMon 收到 USBMon 将调用 IHV 提供 JavaScript，使其执行的端口上连接到基于主机的打印设备的每个 USB 打印作业的 endDocPort 调用任何作业后但在处理该要求。 这可能包括将任何保留的数据发送到设备，并返回 Bidi 架构值来启动手动双工或任何其他 IHV/设备需要的内容。

下图提供了 USB Bidi 扩展体系结构，其中显示该方案的概述其中**getStatus**方法用于从通过 USBPrint 接口设备获取未经请求的状态。

![usb bidi 扩展器体系结构与 getstatus 方法](images/usbbidiext-arch.png)

有关 USB 打印机使用的详细信息，请参阅[USB 打印](usb-printing.md)。

## <a name="usb-bidi-extender-api-reference"></a>USB Bidi 扩展程序 API 参考


USB Bidi 扩展程序中的 JavaScript 代码使用与打印设备进行通信的以下函数：

-   **getSchemas**

-   **setSchema**

-   **getStatus**

-   **requestStatus**

-   **startPrintJob**

-   **writePrintData**

-   **endPrintJob**

有关这些 Api 的详细信息，请参阅[JavaScript API 参考](javascript-api-reference-.md)。

## <a name="usbmon-bidi-extension-xml-schema"></a>USBMon Bidi 扩展 XML 架构


USBMon Bidi 扩展文件使用相同的基本结构为 SNMP Bidi 扩展文件，并 WSDMon Bidi 扩展文件。 在 Windows 驱动程序工具包中发布的 XML 架构文件和 USBMon Bidi 扩展文件会自动进行架构验证 INFGate WHCK 测试过程。 当你在开发 Bidi 扩展架构和使用 USB 总线时，务必注意以下信息：

-   值可以指定 Get、 集或 GetSet 的 accessType。 这表示所述的架构元素在 Bidi Get 或 Set 操作类型的支持的。

-   值可以指定查询密钥。 这应该用于表示用于从设备中获取数据的物理操作。 [打印驱动程序 USB 监视器和 Bidi 示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/print/v4PrintDriverSamples/v4PrintDriver-USBMon-Bidi-Extension)演示支持两个不同 queryKeys 的 USB 设备。 应可在一个 USB 读/写操作中检索相同的查询密钥下的所有属性。

-   如果请求不会立即轮询 Bidi 值 Bidi API 调用中。 RefreshInterval 值是初始的值，该值指示何时在设备上特定 Bidi 架构值的更新中轮询。 每次轮询后 refreshInterval 会增加，直到我们停止轮询。 下面的公式说明如何递增 refreshInterval:

    ```javascript
    currentRefreshInterval = refreshInterval * (3 * numPolls);
    ```

## <a name="usbmon-and-usb-bidi-extension-file-interaction"></a>USBMon 和 USB Bidi 扩展插件文件交互


当创建或打开每个新的 USB 端口，USBMon 将确定连接的设备和关联驱动程序是否包括新的 Bidi 扩展文件和 Bidi 扩展 JavaScriptfile。 USBMon v4 驱动程序清单或驱动程序 INI 文件中搜索和检索文件的名称。 如果 USBMon 找到相关文件，它使用它们来确定此设备支持的扩展 Bidi 架构值的列表，然后与设备来查询它们的值进行通信。 此时 USBMon 支持通过现有的打印后台处理程序 Api 的 IHV 指定 Bidi 架构操作。

## <a name="windows-driver-samples-on-github"></a>GitHub 上的 Windows 驱动程序示例


**USBMon Bidi XML 文件示例**-这提供了 USBMon Bidi 扩展 XML 文件的一个示例。 它使用标准 Bidi 架构属性 DeviceInfo、 配置和内存，还定义了几个自定义扩展插件。 有关详细信息，请参阅[打印驱动程序 USB 监视器和 Bidi 示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/print/v4PrintDriverSamples/v4PrintDriver-USBMon-Bidi-Extension)。

有关 Bibi 扩展文件的详细信息，请参阅[双向通信架构](bidirectional-communication-schema.md)。

**USBMon Bidi JavaScript 文件示例**。 此示例包含一个 USBMon Bidi 扩展器 JavaScript 文件。 它演示了如何支持 Bidi 的 SET 和 GET 操作，以及如何在打印打印机的同时侦听的事件。 有关详细信息，请参阅[打印驱动程序 USB 监视器和 Bidi 示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/print/v4PrintDriverSamples/v4PrintDriver-USBMon-Bidi-Extension)。

调试

可以通过创建以下注册表项启用交互调试。 适用于 USB Bidi JavaScript，打印后台处理程序必须重新启动之前将启用调试。

**项名称：** HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Print

**值名称：** EnableJavaScriptDebugging

**类型：** DWORD

**值：** 1

创建在前面的部分中所示的注册表项，并重新启动托管进程后，该脚本可以进行调试，如下所示：

1. 将调试器附加到宿主进程。 对于 USB Bidi JavaScript，这是 spoolsv.exe。

2. 设置调试器为调试模式下的脚本。

3. 选择"全部中断"（Ctrl + Alt + Break） 若要在下次运行脚本时强行进入该进程。

4. 运行以重现问题的方案。

5. 调试器将中断的 JavaScript 函数后, 设置任何必要的断点并单步执行代码。

## <a name="related-topics"></a>相关主题

[双向通信架构](bidirectional-communication-schema.md)  

[IPrinterBidiSchemaElement](iprinterbidischemaelement-interface.md)  

[IPrinterScriptContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptcontext)  

[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptablesequentialstream)  

[JavaScript API 参考](javascript-api-reference-.md)  

[打印驱动程序 USB 监视器和 Bidi 示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/print/v4PrintDriverSamples/v4PrintDriver-USBMon-Bidi-Extension)  

[USB 打印](usb-printing.md)  

[V4 打印机驱动程序连接](v4-printer-driver-connectivity.md)




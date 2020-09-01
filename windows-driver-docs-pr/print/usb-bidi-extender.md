---
title: USB 双向扩展程序
description: 描述对 USB 设备的双向支持，结合使用双向 XML 文件和称为 USB 双向扩展器的 Javascript 文件。
ms.assetid: C4012369-F1C6-4EBC-8DAE-F4E551DE782D
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 00555e51cfc9c5ec829b16718dc9ad58b9b62718
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212637"
---
# <a name="usb-bidi-extender"></a>USB 双向扩展程序

Windows 允许制造商通过结合使用双向 XML 文件和称为 USB 双向扩展器的 Javascript 文件，为 USB 设备 () 双向通信提供双向通信。

USB 双向扩展器允许应用程序将双向与 USB 结合使用作为传输机制。 在打印过程中，Javascript 实现不支持任何设备流控制或任何包含打印作业的控件信息的多路复用。

默认情况下，双向查询和状态请求通过用于打印的 USB 设备接口进行路由。 这允许使用 **getSchemas** javascript 方法进行状态的完全双向通信，并允许使用 **setSchema** javascript 方法进行设置操作。 如果没有将打印作业发送到打印设备，则可以进行完全双向通信。

在打印过程中，打印作业数据将阻止写入，因此，使用 **getStatus** 方法，只使用读取通道从设备获取未经请求的状态。 但如果设备支持辅助 USB 接口，则在打印设备时，将使用 **requestStatus** 方法函数从打印机获取状态。

在中 Windows 8.1 扩展了 v4 驱动程序模型，以便为基于主机的设备提供支持。 除此之外，USBMon 已更新为允许 Ihv 使用 JavaScript 代码来更好地控制打印路径以及执行打印作业的操作。 更新包括添加提供新的双向 JavaScript 入口点的 Api。 这些 Api 与 USBMon 中的现有函数对齐。

**startPrintJob**。 此新函数与 USBMon 中的 startDocPort 对齐。 在连接到基于主机的打印设备的端口上启动每个新的 USB 打印作业时，USBMon 将调用 IHV 提供的 JavaScript，以允许它执行所需的任何预作业处理。 这可能包括在作业属性包中设置作业全局属性、在设备上查询当前状态和配置数据或不执行任何操作。 完成的任务与设备和 IHV 完全相关。

**writePrintData**。 此新函数与 USBMon 中的 writePort 对齐。 当 USBMon 在打印操作期间从后台处理程序收到每个 writePort 函数调用时，所提供的打印数据需要通过 IHV JavaScript 函数发送到基于主机的设备。 这允许 IHV JS 在此时确定应发送到设备的内容。 IHV 可以根据需要删除、添加或保存部分数据缓冲区。 这允许 IHV 完全控制何时发送到设备。 这会使 IHV 有机会将 (保存在某个永久性) 流中，以便在从后台处理程序接收到所有数据后进行处理，从而帮助启用此类方案作为手动双工。 IHV 还可以使用 printerBidiSchemaResponses 对象来返回处理作业期间的打印作业状态或设备状态。

**endPrintJob**。 此新函数与 USBMon 中的 endDocPort 对齐。 当 USBMon 在连接到基于主机的打印设备的端口上收到每个 USB 打印作业的 endDocPort 调用时，USBMon 将调用 IHV 提供的 JavaScript，以允许它执行所需的任何后处理作业。 这可能包括将任何保留的数据发送到设备、返回双向架构值以开始手动全双工或 IHV/设备需要的任何其他内容。

下图提供了 USB 双向扩展体系结构的概述，其中显示了使用 **getStatus** 方法通过 USBPrint 接口从设备获取未经请求的状态的方案。

![带有 getstatus 方法的 usb 双向扩展器体系结构](images/usbbidiext-arch.png)

有关使用 USB 打印机的详细信息，请参阅 [Usb 打印](usb-printing.md)。

## <a name="usb-bidi-extender-api-reference"></a>USB 双向扩展器 API 参考

USB 双向扩展器中的 JavaScript 代码使用以下功能与打印设备通信：

- **getSchemas**

- **setSchema**

- **getStatus**

- **requestStatus**

- **startPrintJob**

- **writePrintData**

- **endPrintJob**

有关这些 Api 的详细信息，请参阅 [JAVASCRIPT API 参考](javascript-api-reference-.md)。

## <a name="usbmon-bidi-extension-xml-schema"></a>USBMon 双向扩展 XML 架构

USBMon 双向扩展文件使用与 SNMP 双向扩展文件和 WSDMon 双向扩展文件相同的基本结构。 XML 架构文件在 Windows 驱动程序工具包中发布，USBMon 双向扩展文件将在 INFGate WHCK 测试过程中自动进行架构验证。 如果要开发双向扩展架构并使用 USB 总线，请注意以下信息：

- 值可以指定 Get、Set 或 GetSet 的 accessType。 这指示在双向 Get 或 Set 操作类型中支持所述架构元素的位置。

- 值可以指定查询密钥。 这应该用于表示用于从设备获取数据的物理操作。 [打印驱动程序 USB 监视器和双向示例](/samples/microsoft/windows-driver-samples/print-driver-usb-monitor-and-bidi-sample)演示了支持两个不同 QUERYKEYS 的 usb 设备。 同一查询密钥下的所有属性都应该可在一个 USB 读/写操作中进行检索。

- 如果双向 API 调用中请求了双向值，则会立即对它们进行轮询。 RefreshInterval 值为初始值，该值指示何时轮询设备以获取特定双向架构值上的更新。 每次轮询后，refreshInterval 将增加，直到我们停止轮询。 以下公式显示了 refreshInterval 的递增方式：

    ```javascript
    currentRefreshInterval = refreshInterval * (3 * numPolls);
    ```

## <a name="usbmon-and-usb-bidi-extension-file-interaction"></a>USBMon 和 USB 双向扩展文件交互

创建或打开每个新的 USB 端口后，USBMon 将确定附加的设备和关联的驱动程序是否包括新的双向扩展文件和双向扩展 JavaScriptfile。 USBMon 搜索 v4 驱动程序清单或驱动程序 INI 文件，并检索文件的名称。 如果 USBMon 找到相关文件，则会使用它们来确定此设备支持的扩展双向架构值的列表，然后与设备进行通信以查询其值。 此时，USBMon 通过现有的打印后台处理程序 Api 支持 IHV 指定的双向架构操作。

## <a name="windows-driver-samples-on-github"></a>GitHub 上的 Windows 驱动程序示例

**USBMon 双向 XML 文件示例** -这提供了 USBMon 双向扩展 XML 文件的示例。 它使用标准的双向架构属性 DeviceInfo、Configuration 和 Memory，还定义了一些自定义扩展。 有关详细信息，请参阅 [打印驱动程序 USB 监视器和双向示例](/samples/microsoft/windows-driver-samples/print-driver-usb-monitor-and-bidi-sample)。

有关双向扩展文件的详细信息，请参阅 [双向通信架构](bidirectional-communication-schema.md)。

**USBMon 双向 JavaScript 文件示例**。 此示例包括 USBMon 双向扩展程序 JavaScript 文件。 它演示了如何支持双向设置和获取操作，以及如何在打印机打印时侦听事件。 有关详细信息，请参阅 [打印驱动程序 USB 监视器和双向示例](/samples/microsoft/windows-driver-samples/print-driver-usb-monitor-and-bidi-sample)。

调试

可以通过创建以下注册表项来启用交互式调试。 对于 USB 双向 JavaScript，必须重新启动打印后台处理程序，才能启用调试。

**项名称：** HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ 控件 \\ 打印

**值名称：** EnableJavaScriptDebugging

**键入：** DWORD

**值：** 1

在上一节中显示的注册表项被创建并重新启动宿主进程后，可以按以下方式调试该脚本：

1. 将调试器附加到宿主进程。 对于 USB 双向 JavaScript，此 spoolsv.exe。

2. 将调试器设置为脚本调试模式。

3. 选择 " **全部中断** " (Ctrl + Alt + Break) 在脚本下一次运行时中断进程。

4. 运行方案来重现你的问题。

5. 调试器进入 JavaScript 函数后，设置任何必要的断点并单步执行代码。

## <a name="related-topics"></a>相关主题

[双向通信架构](bidirectional-communication-schema.md)  

[IPrinterBidiSchemaElement](iprinterbidischemaelement-interface.md)  

[IPrinterScriptContext](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptcontext)  

[IPrinterScriptableSequentialStream](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream)  

[JavaScript API 参考](javascript-api-reference-.md)  

[打印驱动程序 USB 监视器和双向示例](/samples/microsoft/windows-driver-samples/print-driver-usb-monitor-and-bidi-sample)  

[USB 打印](usb-printing.md)  

[V4 打印机驱动程序连接](v4-printer-driver-connectivity.md)
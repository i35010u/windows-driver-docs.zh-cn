---
title: 自定义 UI 的驱动程序支持
description: V4 打印驱动程序模型是使用打印机扩展或 UWP 设备应用程序的内置支持，用于打印的。
ms.assetid: 91B0E824-1EE3-40B0-A24E-5A66C158972E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc0fd2c18f63a73675889732a2d5f6d9e37af4c6
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802603"
---
# <a name="driver-support-for-customized-ui"></a>自定义 UI 的驱动程序支持


V4 打印驱动程序模型是使用打印机扩展或 UWP 设备应用程序的内置支持，用于打印的。

以下各节介绍了其他 UI 自定义设计注意事项。

**打印首选项**

所有 v4 打印驱动程序都适用于打印首选项。但是，若要确保所有方案之间的最大一致性，请务必维护配置和 UI 层之间的边界。 由于可能没有安装任何打印机扩展或 UWP 设备应用 (或者它们可能已自动安装) ，因此 v4 打印驱动程序需要确保在没有自定义打印机首选项的情况下打印驱动程序正常运行。 具体而言，这意味着在驱动程序的 GPD/PPD + JavaScript 约束实现中，PrintTicket 和 PrintCapabilities 支持应完整且全面。

打印机扩展或 UWP 设备应用中的某些约束验证在提供高信息的交互式体验方面非常有用，但它不应替换驱动程序的验证，这被视为权威。

打印机扩展和 UWP 设备应用应使用 [**IPrinterQueue：： SendBidiQuery**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nf-printerextension-iprinterqueue-sendbidiquery) 方法，而不是对网络资源进行任何直接网络调用。 如果必须联系网络资源，则应在另一个线程上执行此操作，或以异步方式为阻止 UI 溢出。 数据在检索后应缓存，以便更快地调用。

**打印机通知**

打印机通知由双向和 DriverEvent XML 文件驱动。 但为了更好地管理电池寿命和最大程度减少中断，只会在用户打印时显示通知。

虽然打印首选项对于正在打印的应用具有上下文，但打印机通知并不是。 以下流程图说明了 Windows 用于确定打印机通知的行为的决策树。 如果可用，UWP 设备应用优先于打印机扩展。

![打印机通知行为流程图](images/notificationbhvr.png)

**注意**   需要注意的是，如果你尝试使用自定义 UI 通过调用[GetForegroundWindow](https://docs.microsoft.com/windows/win32/api/winuser/nf-winuser-getforegroundwindow)在 Windows 8 环境中显示通知，则将不会显示通知窗口，这一点很重要。 这是因为，操作系统会尝试向使用 GetForegroundWindow 创建前台窗口的线程分配更高的优先级，并且不允许 Windows 8 环境中的对话框使用此操作。 如果要使用自定义 UI 在 Windows 8 环境中显示通知，则必须通过调用 GetDesktopWindow 来执行此操作 [。](https://docs.microsoft.com/windows/win32/api/winuser/nf-winuser-getdesktopwindow)

 

**正在创建驱动程序事件**。 V4 打印驱动程序使用 DriverEvent 的 XML 文件来描述应导致引发驱动程序事件的双向查询和触发器。 请注意，驱动程序事件仅支持标准字符串。 有关标准字符串的详细信息，请参阅 [AsyncUI 默认资源文件字符串资源](https://docs.microsoft.com/openspecs/windows_protocols/ms-pan/cbd34ab3-5a2a-4292-b7ce-e584020d14d7)。 在当前实现中，这将导致使用 [AsyncUIBalloon](https://docs.microsoft.com/openspecs/windows_protocols/ms-pan/9ec494fd-eea8-4545-8e38-5992fa7f6a4a) [协议](https://docs.microsoft.com/openspecs/windows_protocols/ms-pan/e44d984c-07d3-414c-8ffc-f8c8ad8512a8)创建和发布一条消息。 此实现将来可能会更改以提高性能，因此，开发 v4 打印驱动程序以使其不会依赖于基础协议，这一点至关重要。

下图显示了协议利用率。

![使用驱动程序事件的协议利用率](images/drivereventprotutil.png)

**驱动程序事件 XML 示例**。 以下 XML 代码段指定一个驱动程序事件。 事件检查黄色墨迹是否小于双向所报告的总容量的21%。 如果发生这种情况，将使用 resourceID 132 引用的字符串创建 AsyncUIBalloon 消息。 换句话说，消息会说 "%1" 的墨粉/墨不足。 资源 2002 ( "黄色" ) ，将替换为 %1。

```xml
<de:DriverEvents xmlns:de="https://schemas.microsoft.com/windows/2011/08/printing/driverevents" schemaVersion="4.0">
  <DriverEvent eventId="{A04CF0FC-1CEB-4C62-B967-6F0AE5C5F81E}">
    <Transport>USB</Transport>
    <Transport>WSD</Transport>
    <Query>\Printer.Consumables</Query>
    <Trigger result="\Printer.Consumables.Yellow:Level" comparison="LessThan" value="21">
      <StandardMessage resourceId="132">
        <StringParameter index="1" resourceId="2002" />
      </StandardMessage>
    </Trigger>
  </DriverEvent>
</de:DriverEvents>
```

**驱动程序事件架构**。 DriverEvent 架构在 Windows 驱动程序工具包中以 \\ 包含 um PrinterDriverEvents 的形式提供 \\ \\ 。

**驱动程序事件 XML 验证**。 只要在驱动程序清单中正确描述 DriverEvent XML，该 XML 文件就会由 INFGate 工具自动验证。

## <a name="related-topics"></a>相关主题
[AsyncUIBalloon](https://docs.microsoft.com/openspecs/windows_protocols/ms-pan/9ec494fd-eea8-4545-8e38-5992fa7f6a4a)  
[AsyncUI 默认资源文件字符串资源](https://docs.microsoft.com/openspecs/windows_protocols/ms-pan/cbd34ab3-5a2a-4292-b7ce-e584020d14d7)  
[**IPrinterQueue::SendBidiQuery**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nf-printerextension-iprinterqueue-sendbidiquery)  
[MS 平移协议](https://docs.microsoft.com/openspecs/windows_protocols/ms-pan/e44d984c-07d3-414c-8ffc-f8c8ad8512a8)  




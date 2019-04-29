---
title: 自定义 UI 的驱动程序支持
description: V4 打印驱动程序模型开发用于打印的打印机扩展或 UWP 的设备应用程序的 UI 自定义的内置支持。
ms.assetid: 91B0E824-1EE3-40B0-A24E-5A66C158972E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ba91546c62a01b14cb74bbeabfda01343f0bc02
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391958"
---
# <a name="driver-support-for-customized-ui"></a>自定义 UI 的驱动程序支持


V4 打印驱动程序模型开发用于打印的打印机扩展或 UWP 的设备应用程序的 UI 自定义的内置支持。

以下各节中说明了其他 UI 自定义设计注意事项。

**打印首选项**

所有 v4 打印驱动程序都处理打印首选项，但是，务必要维护的配置和 UI 层之间的边界，以便确保所有方案的最大的一致性。 由于可能不存在的任何打印机扩展或安装的 UWP 设备应用程序 （或它们可能已自动安装），v4 打印驱动程序必须确保打印驱动程序的功能，无需自定义的打印机首选项体验。 具体而言，这意味着完整和全面 GPD/PPD + 驱动程序中的 JavaScript 约束实现中，应为 PrintTicket 和 PrintCapabilities 支持。

打印机扩展或 UWP 的设备应用程序中的某些约束验证可能会在提供的高度信息丰富的交互式体验方面非常有用，但它不应取代驱动程序的验证，被视为具有权威。

打印机扩展和 UWP 的设备应用程序应使用[ **IPrinterQueue::SendBidiQuery** ](https://msdn.microsoft.com/library/windows/hardware/hh846197)方法，而不使任何直接的网络调用到网络资源。 如果必须访问网络资源，它应完成另一个线程上或以异步方式以防止 UI 挂起。 检索以更快地使将来的调用后，应缓存数据。

**打印机通知**

打印机通知是由于通过 Bidi 和 DriverEvent XML 文件。 为了更好地管理电池寿命并最大程度减少中断，但是，将仅显示通知时打印用户。

虽然打印首选项有上下文关系的应用程序正在打印，打印机通知不是。 以下流程图解释了 Windows 用于确定打印机通知的行为的决策树。 如果可用，UWP 设备应用程序优先于打印机扩展。

![打印机通知行为流程图](images/notificationbhvr.png)

**请注意**  务必要注意的这一事实，如果您尝试使用自定义 UI 以在 Windows 8 环境中显示一条通知，通过调用[GetForegroundWindow](https://msdn.microsoft.com/library/windows/desktop/ms633505.aspx)，通知窗口不会显示。 这是因为操作系统尝试向创建使用 GetForegroundWindow，前台窗口的线程分配较高的优先级，这不允许对话框在 Windows 8 环境。 如果你想要使用自定义 UI 可在 Windows 8 环境中显示的通知，必须执行此操作通过调用[GetDesktopWindow。](https://msdn.microsoft.com/library/windows/desktop/ms633504.aspx)

 

**创建驱动程序事件**。 V4 打印驱动程序使用 DriverEvent XML 文件来描述 Bidi 查询和触发器的会导致驱动程序事件被引发。 而且，务必要注意的事件驱动程序仅支持标准字符串。 有关标准字符串的详细信息，请参阅[AsyncUI 默认资源文件字符串资源](https://msdn.microsoft.com/library/cc746159.aspx)。 在当前实现中，这将导致[AsyncUIBalloon](https://msdn.microsoft.com/library/cc238009(PROT.10).aspx)消息以进行创建和使用发布[MS 平移协议](https://msdn.microsoft.com/library/cc237960(PROT.13).aspx)。 此实现可能会在将来更改，以提高性能，因此它，请务必开发在 v4 打印驱动程序，以便它不会依赖项的基础协议。

下图显示了协议利用率。

![协议使用率与驱动程序的事件](images/drivereventprotutil.png)

**驱动程序事件的 XML 示例**。 以下 XML 代码段指定一个驱动程序事件。 事件检查 Bidi 报告在小于 21%的总容量的黄色手写内容。 如果发生这种情况，使用引用的资源 Id 132 的字符串创建 AsyncUIBalloon 消息。 换而言之，消息会说，""%1"上很少墨粉/墨水。" 在这里资源 2002 （"黄色"） 将替换为 %1。

```xml
<de:DriverEvents xmlns:de="http://schemas.microsoft.com/windows/2011/08/printing/driverevents" schemaVersion="4.0">
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

**驱动程序事件架构**。 DriverEvent 架构是作为 Windows 驱动程序工具包中可用\\Include\\um\\PrinterDriverEvents.xsd。

**驱动程序事件 XML 验证**。 只要您描述在驱动程序清单中正确 DriverEvent XML，XML 文件进行自动验证 INFGate 工具。

## <a name="related-topics"></a>相关主题
[AsyncUIBalloon](https://msdn.microsoft.com/library/cc238009(PROT.10).aspx)  
[AsyncUI 默认资源文件字符串资源](https://msdn.microsoft.com/library/cc746159.aspx)  
[**IPrinterQueue::SendBidiQuery**](https://msdn.microsoft.com/library/windows/hardware/hh846197)  
[MS 平移协议](https://msdn.microsoft.com/library/cc237960(PROT.13).aspx)  




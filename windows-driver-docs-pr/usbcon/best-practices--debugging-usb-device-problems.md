---
Description: This topic provides tips for debugging USB device problems by using ETW events.
title: 使用 ETW 事件进行调试 USB 设备问题
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f416387697ba48af38bcff2921ec3d2592dd8b28
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541456"
---
# <a name="debugging-usb-device-issues-by-using-etw-events"></a>使用 ETW 事件进行调试 USB 设备问题


本主题提供了使用 ETW 事件进行调试 USB 设备问题的技巧。

-   [诊断设备枚举失败](#diagnosing-device-enumeration-failures)
-   [诊断发生设备启动失败](#diagnosing-device-start-failures)
-   [分析设备插入计时](#profiling-device-insertion-timing)
-   [由软件启动设备恢复计时](#software-initiated-device-resume-timing)
-   [硬件启动设备恢复计时](#hardware-initiated-device-resume-timing)
-   [从选择性中心恢复挂起计时](#hub-resume-from-selective-suspend-timing)

## <a name="diagnosing-device-enumeration-failures"></a>诊断设备枚举失败


可以使用与要确定的大多数设备枚举失败的根本原因的 USB 集线器枚举任务相关联的 ETW 事件。

**若要查看与 USB 集线器枚举任务相关联的跟踪日志中的事件**

1.  开启 Netmon 并查找枚举事件，如"启动的端口的枚举"。 单击中的事件**帧摘要**窗格。
2.  确认此事件的任务是通过检查 USB 集线器枚举**任务**事件字段：
    1.  在中**帧详细信息**窗格中，展开**Net 事件**，展开**标头**，展开**描述符**，然后找到**任务**字段。
    2.  确认任务字段包含的值为 2 （USB 集线器枚举）。

3.  筛选事件以仅显示从中心驱动程序是具有任务值 2:
    1.  右键单击**任务**字段。
    2.  选择**将所选的值添加**到**显示筛选器**。
    3.  右键单击中的事件**帧摘要**窗格，然后选择**添加**到"协议名称"**显示筛选器**。
    4.  在中**显示筛选器**窗格中，更改"OR"到"AND"。 下面的示例显示了生成的筛选器：
        ```cpp
        NetEvent.Header.Descriptor.Task == 0x2 AND ProtocolName == "USBHub_MicrosoftWindowsUSBUSBHUB"
        ```

        使用 Netmon 中筛选器的详细信息，请参阅"USB Netmon 筛选器"中[案例研究：使用 ETW 和 Netmon 未知的 USB 设备进行故障排除](case-study--troubleshooting-an-unknown-usb-device-by-using-etw-and-netmon.md)。

## <a name="diagnosing-device-start-failures"></a>诊断发生设备启动失败


如果设备出现故障，在启动期间中心驱动程序处理的设备的启动 I/O 请求数据包 (IRP)，可以使用 USB 设备启动任务来排查故障与相关联的 ETW 事件。 在网络监视器，查找如"USB 设备启动 IRP 调度"的设备开始事件。 你可以筛选事件以只显示从中心驱动程序任务值为 21 （USB 设备启动）。 创建这样的筛选器的详细信息，请参阅本主题中的"诊断设备枚举失败"。

## <a name="profiling-device-insertion-timing"></a>分析设备插入计时


您可以确定其中所用的时间在中心驱动程序设备插入期间通过观察枚举事件的时间戳。

**枚举计时**

以下两个事件之间经过设备础 丁枚举设备所用的中心驱动程序，是时候的部分：

-   开始枚举端口
-   完成端口的枚举

**分析枚举任务**

当 USB 集线器驱动程序枚举设备时，它按以下顺序记录以下事件：

-   开始枚举端口
-   枚举 Debounce 完成
-   为枚举创建 PDO
-   第一个枚举端口重置完成
-   枚举的完整 CreateDevice
-   第二个枚举端口重置完成
-   枚举的完整 InitializeDevice
-   枚举的完整 SetupDevice
-   完成端口的枚举

若要确定为每个枚举任务中心驱动程序使用的时间，计算前面的事件之间经过的时间。
**IoInvalidateDeviceRelations 和 IRP 之间经过的时间\_MN\_查询\_设备\_关系**

若要确定系统使用时等待查询设备关系 IRP 的设备插入时间部分，测量以下两个事件之间经过的时间：

-   完成端口的枚举
-   USB 集线器查询设备关系 (BusRelations) IRP 调度

**完成的 IRP 之间经过的时间\_MN\_查询\_设备\_关系和 IRP\_MN\_启动\_设备**

若要确定设备插入之间的时间向插管理器和启动 IRP 接收报告的新的物理设备对象 (PDO) 部分，测量以下两个事件之间经过的时间：

-   USB 集线器查询设备关系已完成的 IRP
-   USB 设备开始调度的 IRP

**启动 IRP 计时**

若要确定在处理开始 IRP 的中心驱动程序中所用的时间，度量值的以下两个事件之间经过的时间：

-   USB 设备开始调度的 IRP
-   USB 设备开始完成的 IRP

## <a name="software-initiated-device-resume-timing"></a>由软件启动设备恢复计时


设备的功能驱动程序可以发送 D0 设备电源请求以恢复从挂起状态的设备。 若要确定所需的数量的设备中，若要从挂起中恢复，并准备就绪可供传输请求的时间，度量值的以下两个事件之间经过的时间：

-   USB 设备集 D0 设备电源 IRP 调度
-   USB 设备集 D0 设备电源已完成的 IRP

## <a name="hardware-initiated-device-resume-timing"></a>硬件启动设备恢复计时


总线上的恢复信号会导致设备继续从挂起状态。 若要确定所需的数量的设备，若要恢复到准备好进行传送请求的状态的时间，度量值的以下两个事件之间经过的时间：

-   父中心不会挂起：
    -   USB 设备等待唤醒 IRP 完成
    -   USB 设备集 D0 设备电源已完成的 IRP
-   挂起父中心：
    -   从选择性挂起启动中心恢复 （这些事件的设备和主机控制器之间的任何中心的第一个）
    -   USB 设备集 D0 设备电源已完成的 IRP

## <a name="hub-resume-from-selective-suspend-timing"></a>从选择性中心恢复挂起计时


您可以确定所需的数量的时间为中心继续从选择性挂起通过测量以下两个事件之间经过的时间：

-   启动的恢复的中心从选择性挂起
-   中心已完成的恢复

**请注意**  中心恢复时间取决于中心下的所有设备与上面的集线器的正在恢复可能是某些或所有中心的恢复时间。

 

## <a name="related-topics"></a>相关主题
[USB Windows 事件跟踪](usb-event-tracing-for-windows.md)  




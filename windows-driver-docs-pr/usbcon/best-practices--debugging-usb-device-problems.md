---
description: 本主题提供使用 ETW 事件调试 USB 设备问题的提示。
title: 使用 ETW 事件调试 USB 设备问题
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db74dece457213f3ab588a02388c02ca9fc8f99c
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969004"
---
# <a name="debugging-usb-device-issues-by-using-etw-events"></a>使用 ETW 事件调试 USB 设备问题


本主题提供使用 ETW 事件调试 USB 设备问题的提示。

-   [诊断设备枚举故障](#diagnosing-device-enumeration-failures)
-   [诊断设备启动故障](#diagnosing-device-start-failures)
-   [分析设备插入计时](#profiling-device-insertion-timing)
-   [软件启动的设备恢复计时](#software-initiated-device-resume-timing)
-   [硬件启动的设备恢复计时](#hardware-initiated-device-resume-timing)
-   [集线器从选择性挂起计时中恢复](#hub-resume-from-selective-suspend-timing)

## <a name="diagnosing-device-enumeration-failures"></a>诊断设备枚举故障


您可以使用与 USB 集线器枚举任务关联的 ETW 事件来确定大多数设备枚举失败的根本原因。

**查看与 USB 集线器枚举任务关联的跟踪日志中的事件**

1.  打开 Netmon 并找到枚举事件，如 "开始枚举端口"。 单击 " **帧摘要** " 窗格中的事件。
2.  通过检查事件的 **任务** 字段，确认此事件的任务是 USB 集线器枚举：
    1.  在 " **帧详细信息** " 窗格中，展开 " **网络" 事件**，展开 **标题**，展开 **描述符**，然后找到 " **任务** " 字段。
    2.  确认任务字段包含值 2 (USB 集线器枚举) 。

3.  筛选事件，使其仅显示来自具有任务值2的集线器驱动程序的事件：
    1.  右键单击该 **任务** 字段。
    2.  选择 " **添加所选值** " 以 **显示筛选器**。
    3.  右键单击 " **帧摘要** " 窗格中的事件，然后选择 " **添加**' 协议名称 ' 以 **显示筛选器**"。
    4.  在 " **显示筛选器** " 窗格中，将 "或" 更改为 "AND"。 下面的示例显示了生成的筛选器：
        ```cpp
        NetEvent.Header.Descriptor.Task == 0x2 AND ProtocolName == "USBHub_MicrosoftWindowsUSBUSBHUB"
        ```

        有关在 Netmon 中使用筛选器的详细信息，请参阅 [案例研究：使用 ETW 和 Netmon 对未知 USB 设备进行故障排除](case-study--troubleshooting-an-unknown-usb-device-by-using-etw-and-netmon.md)中的 "USB Netmon 筛选器"。

## <a name="diagnosing-device-start-failures"></a>诊断设备启动故障


如果在集线器驱动程序处理设备的启动 i/o 请求数据包 (IRP) 时设备无法启动，则可以使用与 USB 设备启动任务关联的 ETW 事件来解决失败。 在 Netmon 中，找到设备开始事件，如 "USB 设备启动 IRP 已调度"。 你可以筛选事件，使其仅显示中心驱动程序中的任务值为 21 (USB 设备开始) 。 有关创建此类筛选器的详细信息，请参阅本主题中的 "诊断设备枚举失败"。

## <a name="profiling-device-insertion-timing"></a>分析设备插入计时


您可以通过查看枚举事件的时间戳来确定设备插入期间在集线器驱动程序中花费的时间。

**枚举计时**

用于枚举设备的集线器驱动程序所用的设备插入时间部分是以下两个事件之间的时间：

-   开始枚举端口
-   已完成端口枚举

**分析枚举任务**

当 USB 集线器驱动程序枚举设备时，它会按以下顺序记录以下事件：

-   开始枚举端口
-   枚举反跳已完成
-   为枚举创建的 PDO
-   第一个枚举端口重置完成
-   枚举-CreateDevice 完成
-   第二个枚举端口重置完成
-   枚举-InitializeDevice 完成
-   枚举-SetupDevice 完成
-   已完成端口枚举

若要确定每个枚举任务使用集线器驱动程序的时间，请计算前面的事件之间所间隔的时间。
**IoInvalidateDeviceRelations 和 IRP \_ MN \_ 查询 \_ 设备 \_ 关系之间经过的时间**

若要确定系统在等待查询设备关系 IRP 时使用的设备插入时间部分，请测量以下两个事件之间的运行时间：

-   已完成端口枚举
-    (BusRelations) IRP 的 USB 集线器查询设备关系

**完成 IRP \_ MN \_ 查询 \_ 设备 \_ 关系和 IRP \_ MN \_ 启动 \_ 设备之间经过的时间**

若要确定将新的物理设备对象报告 (PDO) 到即插即用 manager 和接收开始 IRP 之间的设备插入时间部分，请测量以下两个事件之间的运行时间：

-   USB 集线器查询设备关系 IRP 已完成
-   已调度 USB 设备启动 IRP

**启动 IRP 计时**

若要确定在处理开始 IRP 的集线器驱动程序中所花费的时间，请测量以下两个事件之间的运行时间：

-   已调度 USB 设备启动 IRP
-   USB 设备启动 IRP 已完成

## <a name="software-initiated-device-resume-timing"></a>软件启动的设备恢复计时


设备的函数驱动程序可以发送 D0 设备电源请求，使设备从挂起状态恢复。 若要确定设备从暂停状态恢复并准备好传输请求所需的时间，请测量以下两个事件之间经过的时间：

-   USB 设备设置 D0 设备电源 IRP 已调度
-   USB 设备设置 D0 设备电源 IRP 已完成

## <a name="hardware-initiated-device-resume-timing"></a>硬件启动的设备恢复计时


总线上的恢复信号会导致设备从挂起状态恢复。 若要确定设备恢复到已准备好传输请求的状态所需的时间，请测量以下两个事件之间经过的时间：

-   父中心未挂起：
    -   USB 设备等待唤醒 IRP 已完成
    -   USB 设备设置 D0 设备电源 IRP 已完成
-   父中心挂起：
    -   已开始从选择性挂起中恢复集线器 (设备与主机控制器之间任何集线器的这些事件) 
    -   USB 设备设置 D0 设备电源 IRP 已完成

## <a name="hub-resume-from-selective-suspend-timing"></a>集线器从选择性挂起计时中恢复


可以通过测量以下两个事件之间的运行时间来确定中心从选择性挂起恢复所需的时间量：

-   已开始从选择性挂起中恢复集线器
-   已完成集线器恢复

**注意**   集线器恢复计时取决于中心下面所有设备的恢复时间，还可能是正在恢复的中心之上的部分或全部中心。

 

## <a name="related-topics"></a>相关主题
[Windows 的 USB 事件跟踪](usb-event-tracing-for-windows.md)  




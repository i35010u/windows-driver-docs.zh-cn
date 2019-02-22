---
title: HID 概念简介
description: 本部分介绍人机接口设备 （或 HID）。 通常情况下，这些是人们用于直接控制操作的计算机系统的设备。
ms.assetid: 477FF911-5A17-4EA5-9403-1D7B4E8B3BA5
keywords:
- “人机接口设备”
- HID
- 键盘
- 鼠标
- 传感器数据
- 加速感应器
- 陀螺仪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8b30948cea3a3d07b29e1f1843ff683fe11194e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545486"
---
# <a name="introduction-to-hid-concepts"></a>HID 概念简介


本部分介绍人机接口设备 （或 HID）。 通常情况下，这些是人们用于直接控制操作的计算机系统的设备。

## <a name="history-of-hid"></a>HID 的历史记录


Hid 标准的定义通过 USB 设备类作为已启动。 此时目标是定义替换为 PS/2 和通过 USB，从而允许创建键盘、 鼠标和游戏控制器之类的 HID 设备的通用驱动程序创建一个接口。 在之前 HID，设备必须符合的鼠标和键盘的严格定义协议。 所有硬件创新都需要重载中的现有协议的数据使用或需要其自己的驱动程序的非标准硬件。 一种方法查找的操作系统，在这些"启动模式"设备提供基本支持，但仍允许硬件供应商提供具有可扩展、 标准化且易于编程接口的区分入门的 HID 愿景。

目前，HID 设备包括： 字母数字显示、 条形码读取器、 扬声器/耳机、 辅助显示、 传感器和 MRI （是的在医院中） 上的音量控件。 此外，许多硬件供应商的专有设备使用 HID。

HID 通过 USB 启动，但以总线无关的方式从一开始设计。 它最初设计用于低延迟、 低带宽设备但灵活，并且由基础传输指定的速率。 USB 上的 HID 的规范已被批准在 20 世纪 90 年代后期，并在之后不久，启动其他传输通道的支持。 当前，HID 具有一种标准协议在多个传输通道，以及下列传输本机支持在 Windows 8 的 HID:

-   USB
-   蓝牙
-   蓝牙 LE
-   I²C

通过第三方供应商特定传输驱动程序还允许供应商特定的传输。 将在后面几节提供更多详细信息。

## <a name="hid-concepts"></a>HID 的概念


HID 基于几个基本概念、 报告描述符和报告。 报表是在设备和软件客户端之间交换的实际数据 blob。 报表说明符所描述的格式和它所支持的每个数据 blob 的含义。

### <a name="reports"></a>报告

如果应用程序和 HID 设备交换数据，这是通过报告。 有三种报告类型：输入报表，输出将报告，和功能的报表。

| 报告类型    | 描述                                                                                                     |
|----------------|-----------------------------------------------------------------------------------------------------------------|
| 输入的报表   | 从发送 HID 设备到应用程序，通常为控件的状态发生更改时的数据 blob。 |
| 输出报告  | 从发送应用程序到 HID 设备，例如到键盘上的 Led 的数据 blob。         |
| 功能报表 | 数据 blob 可以是手动读取和/或编写的且通常相关配置信息。    |

 

在报表描述符中定义每个顶部级别集合可以包含零 (0) 或每种类型的多个报表。

### <a name="usage-tables"></a>使用表

使用组的 HID 发布一组构成 HID 用法表的文档。 这实际上是描述哪些 HID 设备有权执行此字典。 这些 HID 用法表包含的用法说明的列表。 使用情况向各自的含义和用法的报告描述符中所述的特定项的应用程序开发人员提供信息。 例如，没有定义为左按钮的鼠标的使用情况。 可以定义报表描述符，其中在报表中应用程序可以找到鼠标的左键的当前状态。 使用表已分解成多个命名空间，称为使用情况页面。 每个使用情况页介绍了一组相关的用法，以帮助组织文档。 使用情况页面和使用情况的组合定义唯一标识特定的使用，使用表中的使用情况 ID。

## <a name="the-hid-application-programming-interface-api"></a>HID 应用程序编程接口 (API)


有三个类别的 HID Api： 设备发现和安装程序、 数据移动和报表创建/解释。

### <a name="device-discovery-and-setup"></a>设备发现和安装程序

以下列表标识了应用程序可以使用到 HID API： 确定属性的 HID 设备，并与该设备建立通信。 此外，应用程序可以使用这些 API 的一些用于标识某个顶部级别集合。

-   [**HidD\_GetAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff538900)
-   [**HidD\_GetHidGuid**](https://msdn.microsoft.com/library/windows/hardware/ff538924)
-   [**HidD\_GetIndexedString**](https://msdn.microsoft.com/library/windows/hardware/ff538927)
-   [**HidD\_GetManufacturerString**](https://msdn.microsoft.com/library/windows/hardware/ff538959)
-   [**HidD\_GetPhysicalDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff539677)
-   [**HidD\_GetPreparsedData**](https://msdn.microsoft.com/library/windows/hardware/ff539679)
-   [**HidD\_GetProductString**](https://msdn.microsoft.com/library/windows/hardware/ff539681)
-   [**HidD\_GetSerialNumberString**](https://msdn.microsoft.com/library/windows/hardware/ff539683)
-   [**HidD\_GetNumInputBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff539675)
-   [**HidD\_SetNumInputBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff539686)

### <a name="data-movement"></a>数据移动

以下列表标识的应用程序可以使用该应用程序和所选的设备之间来回移动数据的 HID API。

-   [**HidD\_GetInputReport**](https://msdn.microsoft.com/library/windows/hardware/ff538945)
-   [**HidD\_SetFeature**](https://msdn.microsoft.com/library/windows/hardware/ff539684)
-   [**HidD\_SetOutputReport**](https://msdn.microsoft.com/library/windows/hardware/ff539690)
-   [ReadFile](https://msdn.microsoft.com/library/windows/desktop/aa365467.aspx)
-   [WriteFile](https://msdn.microsoft.com/library/windows/desktop/aa365747.aspx)

### <a name="report-creation-and-interpretation"></a>创建报表和解释

如果你正在编写的 HID 应用为你自己的硬件，则必须的大小和颁发你的设备的每个报表的格式的现有知识。 在这种情况下，您的应用程序可以强制转换的输入和输出到结构报表缓冲区并使用的数据。

如果，但是，要编写与开放常用功能 （例如，音乐应用需要检测何时按下播放按钮） 的所有设备进行通信的 HID 应用，你可能不知道的大小和 HID 报表的格式。 此类别的应用程序理解某些顶部级别集合，因此某些用法。

为了解释从设备收到的报表或创建要发送的报表，该应用程序需要利用报表描述符，以便确定是否在特定使用位于报表和 （如果有） 中的值的单位报表。 这是 HID 分析需要的。 Windows 提供的驱动程序和应用程序使用的 HID 分析器。 此分析器公开一组 Api (HidP\_\*)，可用于发现类型的支持的设备的用法，请确定在报表中，此类使用实例的状态或创建报表以更改状态的设备中的使用情况。

以下列表标识 HID 分析器 Api。

-   [**HidP\_GetButtonCaps**](https://msdn.microsoft.com/library/windows/hardware/ff539707)
-   [**HidP\_GetButtons**](https://msdn.microsoft.com/library/windows/hardware/ff539708)
-   [**HidP\_GetButtonsEx**](https://msdn.microsoft.com/library/windows/hardware/ff539712)
-   [**HidP\_GetCaps**](https://msdn.microsoft.com/library/windows/hardware/ff539715)
-   [**HidP\_GetData**](https://msdn.microsoft.com/library/windows/hardware/ff539718)
-   [**HidP\_GetExtendedAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff539721)
-   [**HidP\_GetLinkCollectionNodes**](https://msdn.microsoft.com/library/windows/hardware/ff539725)
-   [**HidP\_GetScaledUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539729)
-   [**HidP\_GetSpecificButtonCaps**](https://msdn.microsoft.com/library/windows/hardware/ff539733)
-   [**HidP\_GetSpecificValueCaps**](https://msdn.microsoft.com/library/windows/hardware/ff539737)
-   [**HidP\_GetUsages**](https://msdn.microsoft.com/library/windows/hardware/ff539742)
-   [**HidP\_GetUsagesEx**](https://msdn.microsoft.com/library/windows/hardware/ff539745)
-   [**HidP\_GetUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539748)
-   [**HidP\_GetUsageValueArray**](https://msdn.microsoft.com/library/windows/hardware/ff539750)
-   [**HidP\_GetValueCaps**](https://msdn.microsoft.com/library/windows/hardware/ff539754)
-   [**HidP\_InitializeReportForID**](https://msdn.microsoft.com/library/windows/hardware/ff539757)
-   [**HidP\_IsSameUsageAndPage**](https://msdn.microsoft.com/library/windows/hardware/ff539761)
-   [**HidP\_MaxDataListLength**](https://msdn.microsoft.com/library/windows/hardware/ff539768)
-   [**HidP\_MaxUsageListLength**](https://msdn.microsoft.com/library/windows/hardware/ff539770)
-   [**HidP\_SetButtons**](https://msdn.microsoft.com/library/windows/hardware/ff539779)
-   [**HidP\_SetData**](https://msdn.microsoft.com/library/windows/hardware/ff539783)
-   [**HidP\_SetScaledUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539787)
-   [**HidP\_SetUsages**](https://msdn.microsoft.com/library/windows/hardware/ff539792)
-   [**HidP\_SetUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539797)
-   [**HidP\_SetUsageValueArray**](https://msdn.microsoft.com/library/windows/hardware/ff539801)
-   [**HidP\_UnsetButtons**](https://msdn.microsoft.com/library/windows/hardware/ff539812)
-   [**HidP\_UnsetUsages**](https://msdn.microsoft.com/library/windows/hardware/ff539819)
-   [**HidP\_UsageAndPageListDifference**](https://msdn.microsoft.com/library/windows/hardware/ff539824)
-   [**HidP\_UsageListDifference**](https://msdn.microsoft.com/library/windows/hardware/ff539826)

 

 





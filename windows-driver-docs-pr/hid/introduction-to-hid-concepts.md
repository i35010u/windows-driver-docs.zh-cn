---
title: HID 概念简介
description: 本部分介绍了人机接口设备（或 HID）。 通常情况下，这些设备是人们用来直接控制计算机系统操作的设备。
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
ms.openlocfilehash: 19cb06057b4cb9708cd87787a0b6b3c523b17be7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841577"
---
# <a name="introduction-to-hid-concepts"></a>HID 概念简介


本部分介绍了人机接口设备（或 HID）。 通常情况下，这些设备是人们用来直接控制计算机系统操作的设备。

## <a name="history-of-hid"></a>HID 的历史记录


作为 USB 上的设备类启动的 HID 定义。 此时的目标是定义对 PS/2 的替换，并通过 USB 创建一个接口，以允许创建适用于 HID 设备（如键盘、鼠标和游戏控制器）的通用驱动程序。 在 HID 之前，设备必须符合严格定义的用于鼠标和键盘的协议。 所有硬件创新都需要重载现有协议中的数据使用，或创建需要其自己的驱动程序的非标准硬件。 使用 HID 的远景开始，找到一种为操作系统中的 "启动模式" 设备提供基本支持的方法，但仍允许硬件供应商通过可扩展、标准化且易于编程的接口来提供差别。

目前，HID 设备包括：字母数字显示、条形码读者、扬声器/耳机上的音量控制、辅助显示器、传感器和 MRI （是，在医院中）。 此外，许多硬件供应商对其专用设备使用 HID。

在 USB 上启动了 HID，但其开始时间是以总线上不可知的方式设计的。 它最初设计为低延迟、低带宽设备但非常灵活，并且速率由基础传输指定。 在90世纪90年代之前，已批准了基于 USB 的 HID 规范，并且在此之后不久就会开始支持其他传输。 目前，HID 提供了一个标准协议，可通过多个传输在 Windows 8 中以本机方式支持以下传输：

-   “USB”
-   “蓝牙”
-   蓝牙 LE
-   I i2c

还允许通过第三方供应商特定传输驱动程序进行特定于供应商的传输。 稍后部分将提供更多详细信息。

## <a name="hid-concepts"></a>HID 概念


HID 基于几个基本概念、一个报表描述符和报表来构建。 报表是在设备和软件客户端之间交换的实际数据 blob。 报表描述符描述了它支持的每个数据 blob 的格式和含义。

### <a name="reports"></a>报告

当应用程序和 HID 设备交换数据时，可以通过报表完成此操作。 有三种报表类型：输入报表、输出报表和功能报表。

| 报告类型    | 描述                                                                                                     |
|----------------|-----------------------------------------------------------------------------------------------------------------|
| 输入报告   | 从 HID 设备发送到应用程序的数据 blob （通常在控件的状态发生更改时）。 |
| 输出报表  | 从应用程序发送到 HID 设备（例如键盘上的 Led）的数据 blob。         |
| 功能报表 | 可以手动读取和/或写入的数据 blob，通常与配置信息相关。    |

 

报表描述符中定义的每个顶级集合可以包含每个类型的零（0）或更多报表。

### <a name="usage-tables"></a>使用情况表

HID 工作组发布一组文档，这些文档构成了 HID 使用情况表。 这实际上是描述允许哪些 HID 设备执行操作的字典。 这些 HID 用法表包含一个列表，其中包含用法的说明。 使用情况为应用程序开发人员提供有关报表描述符中所述的特定项目的预期含义和用法的信息。 例如，为鼠标的左按钮定义了用法。 报表描述符可以在报表中定义应用程序在何处可以找到鼠标左键的当前状态。 使用情况表分为多个命名空间，称为 "使用情况页"。 每个使用情况页面都描述了一组相关的用法，可帮助组织文档。 "使用情况" 页和 "使用情况" 的组合定义了使用 ID，用于唯一标识用量表中的特定使用情况。

## <a name="the-hid-application-programming-interface-api"></a>HID 应用程序编程接口（API）


有三种类型的 HID Api：设备发现和设置、数据移动和报表创建/解释。

### <a name="device-discovery-and-setup"></a>设备发现和设置

以下列表标识了应用程序可用于：标识 HID 设备的属性以及与该设备建立通信的 HID API。 此外，应用程序还可以使用其中一些 API 来识别顶级集合。

-   [**HidD\_GetAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getattributes)
-   [**HidD\_GetHidGuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_gethidguid)
-   [**HidD\_GetIndexedString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getindexedstring)
-   [**HidD\_GetManufacturerString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getmanufacturerstring)
-   [**HidD\_GetPhysicalDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getphysicaldescriptor)
-   [**HidD\_GetPreparsedData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getpreparseddata)
-   [**HidD\_GetProductString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getproductstring)
-   [**HidD\_GetSerialNumberString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getserialnumberstring)
-   [**HidD\_GetNumInputBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getnuminputbuffers)
-   [**HidD\_SetNumInputBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setnuminputbuffers)

### <a name="data-movement"></a>数据移动

以下列表标识了应用程序可用于在应用程序和所选设备之间来回移动数据的 HID API。

-   [**HidD\_GetInputReport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getinputreport)
-   [**HidD\_SetFeature**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setfeature)
-   [**HidD\_SetOutputReport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setoutputreport)
-   [ReadFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)
-   [WriteFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-writefile)

### <a name="report-creation-and-interpretation"></a>报表创建和解释

如果要为自己的硬件编写 HID 应用，则可以了解设备所颁发的每个报告的大小和格式。 在这种情况下，您的应用程序可以将输入和输出报表缓冲区转换为结构并使用数据。

然而，如果您正在编写一个 HID 应用程序，该应用程序与公开常见功能的所有设备（例如，需要在按下播放按钮时检测的音乐应用程序）进行通信，则您可能不知道 HID 报表的大小和格式。 此类别的应用程序了解某些顶级集合和某些使用情况。

为了解释从设备接收到的报表，或创建要发送的报表，应用程序需要利用报表描述符来确定报表中特定用法的位置和位置，并且（可能为）：报表. 这是需要进行 HID 分析的位置。 Windows 提供了一个 HID 分析器供驱动程序和应用程序使用。 此分析器公开一组 Api （HidP\_\*），这些 Api 可用于发现设备支持的使用类型、确定报表中此类用法的状态，或者生成报表以更改设备中的使用状态。

以下列表标识了 HID 分析器 Api。

-   [**HidP\_GetButtonCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getbuttoncaps)
-   [**HidP\_GetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)
-   [**HidP\_GetButtonsEx**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)
-   [**HidP\_GetCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getcaps)
-   [**HidP\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getdata)
-   [**HidP\_GetExtendedAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getextendedattributes)
-   [**HidP\_GetLinkCollectionNodes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getlinkcollectionnodes)
-   [**HidP\_GetScaledUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getscaledusagevalue)
-   [**HidP\_GetSpecificButtonCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getspecificbuttoncaps)
-   [**HidP\_GetSpecificValueCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getspecificvaluecaps)
-   [**HidP\_GetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages)
-   [**HidP\_GetUsagesEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex)
-   [**HidP\_GetUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevalue)
-   [**HidP\_GetUsageValueArray**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevaluearray)
-   [**HidP\_GetValueCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getvaluecaps)
-   [**HidP\_InitializeReportForID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_initializereportforid)
-   [**HidP\_IsSameUsageAndPage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_usage_and_page)
-   [**HidP\_MaxDataListLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_maxdatalistlength)
-   [**HidP\_MaxUsageListLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_maxusagelistlength)
-   [**HidP\_SetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)
-   [**HidP\_SetData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setdata)
-   [**HidP\_SetScaledUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setscaledusagevalue)
-   [**HidP\_SetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)
-   [**HidP\_SetUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevalue)
-   [**HidP\_SetUsageValueArray**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevaluearray)
-   [**HidP\_UnsetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)
-   [**HidP\_UnsetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages)
-   [**HidP\_UsageAndPageListDifference**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff539824(v=vs.85))
-   [**HidP\_UsageListDifference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_usagelistdifference)

 

 





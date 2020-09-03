---
title: 测试存在还是需要自定义 WDTF 简单 i/o 操作插件
description: 如果已使用 Visual Studio 配置了用于测试的远程计算机，则可以运行一个实用工具测试，该测试显示具有 WDTF 简单 i/o 插件的所有设备。
ms.assetid: 7AD2F8DD-8428-4C30-A3B0-B6678986DCCD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2ca890568d118430f3771e6773902d3520b1f30
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402666"
---
# <a name="how-to-determine-if-a-custom-wdtf-simple-io-action-plug-in-is-required-for-your-device"></a>如何确定设备是否需要自定义 WDTF 简单 i/o 操作插件


如果已使用 Visual Studio 配置了用于测试的远程计算机，则可以运行一个实用工具测试，该测试显示具有 WDTF 简单 i/o 插件的所有设备。该测试还返回测试计算机上没有 WDTF 简单 i/o 支持的设备的列表。 如果你的设备不受支持，则可以使用 **WDTF 简单的 I/o 操作插件** 模板在 Visual Studio 中创建一个，请参阅 [如何使用 WDTF 简单 i/o 操作插件为你的设备自定义 i/o](to-customize-i-o-for-your-device-using-the-wdtf-simple-i-o-action-plug-in.md)。

### <a name="prerequisites"></a>先决条件

-   测试中的设备已安装在测试计算机上。
-   在测试计算机上对其进行测试签名和安装的驱动程序包。 若要验证是否正确安装了驱动程序，请参阅如何测试驱动程序包。
-   测试针对部署配置和预配的计算机。 请参阅 [使用 Visual Studio 在运行时测试驱动程序](/windows-hardware/drivers)

<a name="instructions"></a>Instructions
------------

### <a name="test-your-device-to-see-if-you-need-to-customize-the-wdtf-simple-io-action-plug-in"></a>测试您的设备，查看是否需要自定义 WDTF 简单 i/o 操作插件

WDK 提供一项实用程序测试，你可以运行该测试来确定设备类型是否有 WDTF 简单的 i/o 插件。

1.  打开 **驱动程序测试组资源管理器**。 从 "驱动程序" 菜单中，单击 " **驱动程序 &gt; 测试 &gt; 驱动程序测试组资源管理器**"
2.  创建新的测试组。
3.  在 "驱动程序测试组" 窗口中，单击 " **添加/删除测试**"。
4.  在 "**添加或删除测试**" 对话框中，从 "**设备测试类别**" 列表中选择 "**所有测试" \\ 实用程序**，然后添加**具有 WDTF 简单 i/o 插件的测试显示设备**。单击 **"确定"**。 保存测试组。
5.  运行包含实用程序测试 **显示设备（具有 WDTF 简单 i/o 插件）** 的测试组。
6.  打开测试的 TestTextlog，并验证是否已将设备报告为具有 WDTF 简单 i/o 插件的设备。 如果设备已列出，则无需为设备创建简单的 i/o 插件。 你可以运行设备基础测试，并将自动选择设备类型的正确插件。 有关提供的测试的信息，请参阅 [如何选择和配置设备基础测试](/windows-hardware/drivers)。

    如果设备没有 i/o 插件，需要通过自定义 WDTF 简单的 "i/o 操作" 插件模板来创建一个。

**示例测试文本日志**

``` syntax
WDTF_TEST                 : INFO  : 
WDTF_TEST                 : INFO  :  Devices that we do NOT have a simple I/O Plug-in for
WDTF_TEST                 : INFO  : 
WDTF_TEST                 : INFO  :      Intel(R) ICH10 Family USB Universal Host Controller - 3A68 PCI\VEN_8086&DEV_3A68&SUBSYS_3035103C&REV_02\3&33FD14CA&0&D1 
WDTF_TEST                 : INFO  :      Generic Non-PnP Monitor DISPLAY\DEFAULT_MONITOR\5&1934D7DD&0&UID259 

....

WDTF_TEST                 : INFO  :  Devices that we have a simple I/O Plug-in for
WDTF_TEST                 : INFO  : 
WDTF_TEST                 : INFO  :      Generic volume (I:) STORAGE\VOLUME\{A6EA1A2E-87E6-11E1-9834-806E6F6E6963}#0000006F7FD00000
WDTF_TEST                 : INFO  :      Generic volume (G:) STORAGE\VOLUME\_??_USBSTOR#DISK&VEN_GENERIC&PROD_STORAGE_DEVICE&REV_9744#000000000010&2#{53F56307-B6BF-11D0-94F2-00A0C91EFB8B} 

..... 

```

## <a name="related-topics"></a>相关主题
[How to customize I/O for your device using the WDTF Simple I/O Action Plug-in](to-customize-i-o-for-your-device-using-the-wdtf-simple-i-o-action-plug-in.md)（如何使用 WDTF 简单 I/O 操作插件为设备自定义 I/O）  
[Provided WDTF Simple I/O plug-ins](provided-wdtf-simpleio-plug-ins.md)（提供的 WDTF 简单 I/O 插件）
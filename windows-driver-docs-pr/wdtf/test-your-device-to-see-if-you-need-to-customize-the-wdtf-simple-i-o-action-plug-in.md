---
title: 测试存在或需要自定义 WDTF 简单 I/O 操作插件
description: 如果已配置为使用 Visual Studio 测试的远程计算机，可以运行一个实用程序测试，以便显示所有具有 WDTF 简单 I/O 插件的设备。
ms.assetid: 7AD2F8DD-8428-4C30-A3B0-B6678986DCCD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8600413245042e609773c27f3889740ca61665f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369479"
---
# <a name="how-to-determine-if-a-custom-wdtf-simple-io-action-plug-in-is-required-for-your-device"></a>如何确定自定义 WDTF 简单 I/O 操作插件是否需要为你的设备


如果已配置为使用 Visual Studio 测试的远程计算机，可以运行一个实用程序测试，以便显示所有具有 WDTF 简单 I/O 插件的设备。该测试还返回不具有 WDTF 简单 I/O 支持的测试计算机上的设备的列表。 如果不支持你的设备，则可以创建一个 Visual Studio 中使用**WDTF 简单 I/O 操作插件**模板，请参阅[如何为你的设备使用 WDTF 简单 I/O 操作插件自定义 I/O](to-customize-i-o-for-your-device-using-the-wdtf-simple-i-o-action-plug-in.md)。

### <a name="prerequisites"></a>先决条件

-   在测试计算机上安装待测试的设备。
-   是测试签名，并且在测试计算机上安装的驱动程序包。 若要验证您的驱动程序正确安装，请参阅如何测试驱动程序包。
-   测试针对部署配置和预配的计算机。 请参阅[测试在运行时使用 Visual Studio 的驱动程序](https://docs.microsoft.com/windows-hardware/drivers)

<a name="instructions"></a>说明
------------

### <a name="test-your-device-to-see-if-you-need-to-customize-the-wdtf-simple-io-action-plug-in"></a>测试你的设备以查看您是否需要自定义 WDTF 简单 I/O 操作插件

WDK 提供了实用程序测试可以运行以确定是否有用于你的设备类型的插件 WDTF 简单 I/O。

1.  打开**驱动程序测试组资源管理器**。 从驱动程序菜单中，单击**驱动程序&gt;测试&gt;驱动程序测试组资源管理器**。
2.  创建新的测试组。
3.  在驱动程序测试组窗口中，单击**添加/删除测试**。
4.  在中**添加或删除测试**对话框中，选择**的所有测试\\实用程序**从**设备测试类别**列表，然后添加测试**显示具有 WDTF 简单 I/O 插件的设备**。单击“确定”  。 保存测试组。
5.  运行包括实用程序测试的测试组**显示了 WDTF 简单 I/O 插件设备**。
6.  打开测试 TestTextlog 并验证你的设备被报告为具有 WDTF 简单 I/O 的插件的设备。 如果列出你的设备，则你不需要创建一个简单的 I/O 插件为你的设备。 您可以运行设备基础测试和正确为你的设备类型将自动选择插件。 提供测试有关的信息，请参阅[如何选择和配置设备基础测试](https://docs.microsoft.com/windows-hardware/drivers)。

    如果没有任何 I/O 插件为你的设备，需要创建一个自定义提供的 WDTF 简单 I/O 操作插件模板。

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




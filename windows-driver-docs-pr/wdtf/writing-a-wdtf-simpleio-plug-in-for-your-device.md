---
title: 为设备编写 WDTF 简单的 i/o 插件
description: 若要充分利用设备基础测试，你的设备应当有一个可以对设备执行简单 I/O 操作的简单 I/O 插件。
ms.assetid: FAC4D538-4C2B-46C1-B971-63FF66C2922B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff259127f59f1f9b0039fc1d8aa8c98ef1a44631
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402878"
---
# <a name="writing-a-wdtf-simple-io-plug-in-for-your-device"></a>为设备编写 WDTF 简单的 i/o 插件

若要充分利用[设备基础测试](../develop/how-to-select-and-configure-the-device-fundamental-tests.md)，你的设备应当有一个可以对设备执行简单 I/O 操作的简单 I/O 插件。 这可以是 WDTF 附带的默认简单 I/O 插件之一，也可以是你自己编写的插件。 若要了解设备类型是否受支持以及确定是否有特定的测试要求，请参阅[提供的 WDTF 简单 I/O 插件](provided-wdtf-simpleio-plug-ins.md)。

如果已使用 Visual Studio 配置了测试计算机用于测试，则可以运行一个测试，该测试会返回测试计算机上具有 WDTF 简单 i/o 支持的设备的列表。 如果你的设备不受支持，则可以使用 **WDTF Simple I/o 操作插件** 模板在 Visual Studio 中创建一个。 有关信息，请参阅 [如何使用 WDTF Simple I/o 操作插件自定义设备的 i/o](to-customize-i-o-for-your-device-using-the-wdtf-simple-i-o-action-plug-in.md)。 有关设置测试计算机的信息，请参阅设置 [计算机以进行驱动程序部署和测试 (WDK 10) ](../gettingstarted/provision-a-target-computer-wdk-8-1.md)。

## <a name="in-this-section"></a>本节内容

- [如何确定设备是否需要自定义 WDTF 简单 i/o 操作插件](test-your-device-to-see-if-you-need-to-customize-the-wdtf-simple-i-o-action-plug-in.md)

- [How to customize I/O for your device using the WDTF Simple I/O Action Plug-in](to-customize-i-o-for-your-device-using-the-wdtf-simple-i-o-action-plug-in.md)（如何使用 WDTF 简单 I/O 操作插件为设备自定义 I/O）

- [提供的 WDTF SimpleIO 插件](provided-wdtf-simpleio-plug-ins.md)
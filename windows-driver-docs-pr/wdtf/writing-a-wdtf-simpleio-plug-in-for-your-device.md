---
title: 编写 WDTF 简单 I/O 的设备的插件
description: 若要从设备基础测试获取最大效益，你的设备应具有简单 I/O 插件可以执行简单 I/O 向你的设备。
ms.assetid: FAC4D538-4C2B-46C1-B971-63FF66C2922B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51dc254ab2a6bcfb3deb6fa4f6db1c90ce12ef7a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567374"
---
# <a name="writing-a-wdtf-simple-io-plug-in-for-your-device"></a>编写 WDTF 简单 I/O 的设备的插件

若要充分利用[设备基础测试](https://docs.microsoft.com/windows-hardware/drivers/develop/how-to-select-and-configure-the-device-fundamental-tests)，你的设备应当有一个可以对设备执行简单 I/O 操作的简单 I/O 插件。 这可以是 WDTF 附带的默认简单 I/O 插件之一，也可以是你自己编写的插件。 若要了解设备类型是否受支持以及确定是否有特定的测试要求，请参阅[提供的 WDTF 简单 I/O 插件](provided-wdtf-simpleio-plug-ins.md)。

如果已配置为使用 Visual Studio 测试的测试计算机，可以运行一个测试，以便返回具有 WDTF 简单 I/O 支持的测试计算机上的设备的列表。 如果不支持你的设备，则可以创建一个 Visual Studio 中使用**WDTF 简单 I/O 操作插件**模板。 有关信息，请参阅[如何为你的设备使用 WDTF 简单 I/O 操作插件自定义 I/O](to-customize-i-o-for-your-device-using-the-wdtf-simple-i-o-action-plug-in.md)。 有关设置测试计算机的信息，请参阅[预配计算机，以使驱动程序部署和测试 (WDK 10)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)。

## <a name="in-this-section"></a>本节内容

- [如何确定自定义 WDTF 简单 I/O 操作插件是否需要为你的设备](test-your-device-to-see-if-you-need-to-customize-the-wdtf-simple-i-o-action-plug-in.md)

- [How to customize I/O for your device using the WDTF Simple I/O Action Plug-in](to-customize-i-o-for-your-device-using-the-wdtf-simple-i-o-action-plug-in.md)（如何使用 WDTF 简单 I/O 操作插件为设备自定义 I/O）

- [提供 WDTF SimpleIO 插件](provided-wdtf-simpleio-plug-ins.md)

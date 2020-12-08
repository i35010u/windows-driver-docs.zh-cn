---
title: 使用 WDF 选项卡的设备
description: 本主题讨论使用 WDF 的 WDF 验证程序的设备。
keywords:
- WDF 验证程序 WDK，管理 KMDF 设置
- KMDF 验证程序设置 WDK WDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 004d8d6680d3179c1677095c86ae3bcd9ea23aba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839027"
---
# <a name="devices-using-wdf-tab"></a>使用 WDF 选项卡的设备


本主题讨论 **使用 wdf** 的 wdf 验证程序的设备。 此页列出了使用 WDF 驱动程序的所有设备。 突出显示设备时，将看到突出显示的设备的 WDF 驱动程序堆栈。 你还可以通过此屏幕更改验证设置。

在此页的顶部，可以找到已安装的运行时和驱动程序的摘要。 下面是与 WDF 驱动程序关联的设备实例的列表。

![使用 wdf 选项卡获取设备的屏幕截图](images/wdfverifier-tab2.png)

在 " **使用 wdf 驱动程序的设备** " 框中，具有 wdf 相关设置的设备前面有一个 +。 若要更改设置，请右键单击设备 ID 或节点内的各个设置。

选择设备或单个设置后，设备的友好名称将出现在框的右侧。

此外，该设备的所有 WDF 驱动程序都显示在 " **此设备的 Wdf 驱动程序堆栈** " 框中，按从上到下的堆栈顺序显示。 例如，上层筛选器显示在顶部，后面依次是函数驱动程序和筛选器。

如果使用 UMDF 驱动程序，则它们也会按堆栈顺序显示在内核设备堆栈中的正确位置。

同样，您可以在驱动程序堆栈中单击 "+" 以打开节点，然后右键单击以更改每个驱动程序的值。

如果你在 **使用 wdf 的设备** 上进行更改，则会看到这些更改反映在 **WDF 驱动程序** 页面上。

 

 






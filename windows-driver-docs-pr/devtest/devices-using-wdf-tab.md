---
title: 使用 WDF 选项卡上的设备
description: 本主题讨论使用 WDF 页 WDF 验证程序的设备。
ms.assetid: 06144cf4-bb6f-4b5b-ac0d-f4fae89a04a9
keywords:
- WDF 验证程序 WDK，管理 KMDF 设置
- KMDF 验证器设置 WDK WDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4a1aad9820544f91c4c9be23197bf43db1aca2a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521815"
---
# <a name="devices-using-wdf-tab"></a>使用 WDF 选项卡上的设备


本主题讨论了 WDF Verifier**使用 WDF 设备**页。 此页列出了使用 WDF 驱动程序的所有设备。 在突出显示设备，可以看到突出显示设备的 WDF 驱动程序堆栈。 在此屏幕中，您还可以更改验证设置。

在此页顶部，您会发现已安装运行时和驱动程序的摘要。 下面是与 WDF 驱动程序相关联的设备实例的列表。

![方的设备使用 wdf 选项卡的屏幕截图](images/wdfverifier-tab2.png)

在中**WDF 驱动程序的设备**框中，具有与 WDF 相关的设置的设备的前面有 +。 若要更改设置，请右键单击设备 ID 或节点中的单个设置。

当你选择的设备或单个设置时，设备的友好名称将显示右侧的框。

此外，所有设备的 WDF 驱动程序所示**WDF 驱动程序堆栈为此设备**框中，在堆栈顺序，从上到下。 例如，上部的筛选器出现在顶部后, 跟函数驱动程序，然后降低筛选器。

如果使用 UMDF 驱动程序，他们还会看到在中，内核设备堆栈中的正确位置堆栈顺序。

同样，您可以单击 + 驱动程序堆栈，以打开节点中，然后右键单击要更改每个驱动程序的值。

如果在上进行更改**设备使用 WDF**页上，你会看到上反映这些变化**WDF 驱动程序**页。

 

 






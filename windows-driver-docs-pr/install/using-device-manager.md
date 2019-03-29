---
title: 适合设备和驱动程序制造商的设备管理器
description: 设备管理器提供了驱动程序和设备安装问题的解决方法。
ms.assetid: 3c229347-b36f-43e7-9e9c-3ba6ec1e6108
keywords:
- 设备管理器 WDK
- 设备管理器 WDK，有关设备管理器
ms.date: 10/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: fd6c8f99d2ad97ac2ea676ccae48118c5fc212a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575865"
---
# <a name="using-device-manager"></a>使用设备管理器

若要启动设备管理器中，在文件资源管理器中，右键单击**此电脑**，单击**管理**，然后选择**设备管理器**列出在随后出现的系统工具对话框。

设备管理器显示有关每个设备的信息。 这包括设备类型、 设备状态、 制造商、 特定于设备的属性和设备的驱动程序有关的信息。

如果你的设备需要来启动计算机，你的设备安装问题可以阻止计算机启动。 在这些情况下，您必须使用内核调试程序排查设备安装问题。 有关详细信息，请参阅[开始使用 WinDbg （内核模式）](https://docs.microsoft.com/windows-hardware/drivers/debugger/getting-started-with-windbg--kernel-mode-)。

如果你的设备不需要启动计算机，设备管理器将一个黄色感叹号接下来该设备的名称在设备管理器对话框。 设备管理器还提供了描述问题的错误消息。 有关错误消息的详细信息，请参阅[设备管理器错误消息](device-manager-error-messages.md)。

设备管理器可以显示隐藏的设备。 在测试新的即插即用设备安装时，这非常有用。 有关详细信息，请参阅[查看隐藏的设备](viewing-hidden-devices.md)。

设备管理器提供了每个设备的属性对话框中的详细的信息。 右键单击设备的名称，然后单击**属性**。 **常规**，**驱动程序**，**详细信息**，以及**事件**选项卡包含调试错误时非常有用的信息。 有关详细信息，请参阅[设备管理器详细信息选项卡](device-manager-details-tab.md)。

---
title: 初始化 UMDF 驱动程序
description: 初始化 UMDF 驱动程序
ms.assetid: b21ec019-1a80-4219-8aa8-3545ec3383b9
keywords:
- 用户模式驱动程序框架 WDK，初始化驱动程序
- UMDF WDK，初始化驱动程序
- 用户模式驱动程序 WDK UMDF，初始化
- 初始化 WDK UMDF 驱动程序
- 发送程序 WDK UMDF
- 正在加载发送程序 WDK UMDF
- 驱动程序主机进程 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e35ad6691542b5a704f166556ea50137739b8d8c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534258"
---
# <a name="initializing-umdf-drivers"></a>初始化 UMDF 驱动程序


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

设备的 UMDF 驱动程序初始化之前，由操作系统加载驱动程序管理器和该发送程序和驱动程序主机进程创建。 若要确保设备启动成功，驱动程序管理器进行加载和完全初始化该发送程序初始化时。

安装设备时，插 (PnP) 子系统加载该发送程序，如果不是已加载中。 然后，该发送程序联系要创建驱动程序主机进程的驱动程序管理器。 新创建的驱动程序主机内 framework 处理然后调用[ **IDriverEntry::OnInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff554900)方法来初始化 UMDF 驱动程序，如果尚未初始化。

框架将添加一个新的设备驱动程序主机进程中加载每个设备对象。 以下部分显示概述，并提供有关框架如何添加新设备详细信息：

-   [添加设备概述](adding-a-device-overview.md)
-   [添加设备](adding-a-device.md)

 

 






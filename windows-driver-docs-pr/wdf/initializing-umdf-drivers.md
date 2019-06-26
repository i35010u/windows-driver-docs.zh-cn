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
ms.openlocfilehash: 87a20f294192864106fceae48587ec8ba53e56bd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371144"
---
# <a name="initializing-umdf-drivers"></a>初始化 UMDF 驱动程序


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

设备的 UMDF 驱动程序初始化之前，由操作系统加载驱动程序管理器和该发送程序和驱动程序主机进程创建。 若要确保设备启动成功，驱动程序管理器进行加载和完全初始化该发送程序初始化时。

安装设备时，插 (PnP) 子系统加载该发送程序，如果不是已加载中。 然后，该发送程序联系要创建驱动程序主机进程的驱动程序管理器。 新创建的驱动程序主机内 framework 处理然后调用[ **IDriverEntry::OnInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-oninitialize)方法来初始化 UMDF 驱动程序，如果尚未初始化。

框架将添加一个新的设备驱动程序主机进程中加载每个设备对象。 以下部分显示概述，并提供有关框架如何添加新设备详细信息：

-   [添加设备概述](adding-a-device-overview.md)
-   [添加设备](adding-a-device.md)

 

 






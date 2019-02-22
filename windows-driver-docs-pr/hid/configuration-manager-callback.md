---
title: 配置管理器回调
description: 配置管理器回调
ms.assetid: a8d33bed-3a06-4d61-be42-b9ae195b79f9
keywords:
- 回调 WDK 游戏杆
- 配置管理器回调 WDK 游戏杆
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3ed725d6a60cdad5027d420d2b479a3c6242b834
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533536"
---
# <a name="configuration-manager-callback"></a>配置管理器回调





```cpp
CONFIGRET CM_HANDLER CfgRoutine( CONFIGFUNC cfFuncName, 
    SUBCONFIGFUNC scfSubFuncName, DEVNODE dnToDevNode, 
    ULONG dwRefData, ULONG ulFlags );
```

我部分的 Windows 的即插即用和播放环境部分中提供了有关如何配置管理器的常规信息的 Windows 驱动程序开发工具包 (DDK)。 (在 DDK 前面带有 Windows Driver Kit \[WDK\]。)

配置管理器回调传递给微型驱动程序中，仅当 VJoyD 接收回调时，微型驱动程序会加载。 正因为如此重大问题存在具有此回调的当前实现。 VJoyD 接收回调它与之关联的设备节点枚举在系统启动期间时 configuration manager 在设备重新配置，如的特殊事件的运行时发送一条消息，并在系统时这些设备节点关闭。 因此，仅选择在上一次启动设备加载要接收这些消息的时间。 这将限制时调用该回调时，因为用户可以启动系统，配置游戏杆、 玩游戏、 取消配置游戏杆和关闭而不会调用此回调的情况下，将执行的函数的潜在数量。

对于不需要任何硬件资源的设备，这不是问题。 使用此类资源的设备有多个选项： 其可仅当在启动时配置时，它们可以从 configuration manager 中，动态分配的资源或他们可以为其分配自己的设备节点在注册表中进行搜索和请求的信息。

给定上述信息后，驱动程序正确初始化时首次加载该驱动程序并接收 SYS\_动态\_设备\_INIT，或在第一次通过轮询例程。 同样，资源应进行免费时 SYS\_动态\_设备\_收到退出消息。

另一个问题是，所有的配置管理器回调的当前服务游戏杆设备发送到所有已加载的微型驱动程序。 但是，可以使用*dnToDevNode*参数，以查找设备标识符，并且可以检查对此驱动程序可以处理的设备。

 

 





---
title: 用于启用调试的启动参数
description: 用于启用调试的启动参数
ms.assetid: acbe2fcd-6f8f-49c8-9de6-1617a1723cf5
keywords:
- 启动参数 WDK
- 启动项参数 WDK
- 内核调试支持 WDK 启动选项
- 本地调试 WDK 启动参数
- 单计算机调试 WDK 启动参数
- 数据调试 WDK 启动参数
- IEEE 1394 电缆 WDK 启动参数
- 1394连接 WDK 启动参数
- USB 2.0 调试连接 WDK 启动参数
- 空调制解调器电缆 WDK 启动参数
ms.date: 09/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: 802f465b56b4401d46444624c91967d171bd33d4
ms.sourcegitcommit: a1b2e27c3487a099180fb928f64e7ce3d94f21a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "90846534"
---
# <a name="boot-parameters-to-enable-debugging"></a>用于启用调试的启动参数

建立内核调试连接时，系统会向内核调试器控制其执行。 此外，当发生 bug 检查或内核模式程序与调试器通信时，计算机会等待内核调试器的响应，然后再继续。

> [!IMPORTANT]
> 手动设置网络调试是一种复杂且容易出错的过程。
> 若要自动设置网络调试，请参阅 **[自动设置 KDNET 网络内核调试](../debugger/setting-up-a-network-debugging-connection-automatically.md)**。 **强烈**建议所有调试器用户使用 KDNET 实用程序。

有关手动设置网络连接的信息，请参阅 [通过网络电缆手动设置内核模式调试](../debugger/setting-up-a-network-debugging-connection.md)。

>[!Note]
> 设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。

你可以使用 **bcdedit** 命令查看当前的调试器启动项并更改其设置。 有关更多详细信息，请参阅 [**bcdedit/debug**](./bcdedit--debug.md) 和 [**bcdedit/dbgsettings**](./bcdedit--dbgsettings.md)。

## <a name="boot-parameters-to-debug-the-boot-process-in-windows"></a>用于在 Windows 中调试启动过程的启动参数

若要启用启动调试，请使用 [**BCDEdit/bootdebug**](./bcdedit--bootdebug.md) 命令，并指定相应的启动组件。 如果要在 Windows 启动后执行内核调试，还应使用 [**BCDEdit/debug**](./bcdedit--debug.md) 命令。 还必须选择调试连接，就像在正常内核调试中一样。 有关更多详细信息，请参阅 [**BCDEdit/bootdebug**](./bcdedit--bootdebug.md)。

<a name="see-also"></a>请参阅
--------

有关 Windows 调试工具的信息，请参阅 [Windows 调试](../debugger/index.md)。

有关设置和配置内核模式调试会话的信息，请参阅 [手动设置内核模式调试](../debugger/setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md) 和 [自动设置 KDNET 网络内核调试](../debugger/setting-up-a-network-debugging-connection-automatically.md)。
---
title: 通过类安装程序和辅助安装程序修改注册表项
description: 通过类安装程序和辅助安装程序修改注册表项
ms.assetid: A7F41F97-5E06-41d8-B80F-DDBC41A62BB3
keywords:
- 注册表 WDK 设备安装，修改注册表项
- 注册表 WDK 设备安装，修改注册表项，类安装程序
- 注册表 WDK 设备安装，修改注册表项，共同安装程序
- 类安装程序 WDK 设备安装，修改注册表项
- 共同安装程序 WDK 设备安装，修改注册表项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60b42807ce094f66307a1bb596a90dfed1fc35e0
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733256"
---
# <a name="modifying-registry-keys-by-class-installers-and-co-installers"></a>通过类安装程序和辅助安装程序修改注册表项


**注意**   通用或移动驱动程序包不支持本部分中介绍的功能。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

除非在某些情况下， *类安装* 程序和 *共同安装程序* 不应使用标准注册表函数来创建、更改或删除注册表项。 在大多数情况下，只能使用放在 [INF 文件](overview-of-inf-files.md)中的指令来修改注册表项。 有关这些指令的详细信息，请参阅 [INF 指令摘要](summary-of-inf-directives.md)。

下面是此规则的例外情况：

-   必要时，类安装程序和共同安装程序可以使用标准注册表功能修改 **HKLM \\ 软件** 子树中的注册表项。

    **注意**   我们强烈建议类安装程序和共同安装程序将自定义设备属性保存为设备的*软件密钥*中的条目。

     

-   允许类安装程序和共同安装程序修改 **HKLM \\ System \\ CurrentControlSet \\ Control \\ CoDeviceInstallers** 注册表项中的子项。

应遵循以下准则，以安全地修改类安装程序或共同安装程序的注册表项：

-   类安装程序和共同安装程序必须首先使用 [**SetupDiCreateDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdicreatedevregkeya) 或 [**SetupDiOpenDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdiopendevregkey) 来打开要修改的注册表项的句柄。 打开句柄后，类安装程序和共同安装程序可以使用标准注册表函数来修改注册表项。

-   类安装程序和共同安装程序不得对设备使用 **SetupDiDeleteDevRegKey** 或 *硬件密钥* 。 有关详细信息，请参阅 [删除设备的注册表项](deleting-the-registry-keys-of-a-device.md)。

有关标准注册表函数的详细信息，请参阅 [注册表函数](/windows/win32/sysinfo/registry-functions)。


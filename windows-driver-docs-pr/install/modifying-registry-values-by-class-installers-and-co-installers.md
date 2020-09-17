---
title: 通过类安装程序和辅助安装程序修改注册表值
description: 通过类安装程序和辅助安装程序修改注册表值
ms.assetid: 2D4B907A-622B-4b1b-A692-8E858F770F70
keywords:
- 注册表 WDK 设备安装，修改注册表值
- 注册表 WDK 设备安装，修改注册表值，类安装程序
- 注册表 WDK 设备安装，修改注册表值，共同安装程序
- 类安装程序 WDK 设备安装，修改注册表值
- 共同安装程序 WDK 设备安装，修改注册表值
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e870dab7cea31d6bbb7412b1989505439d5d68d
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717278"
---
# <a name="modifying-registry-values-by-class-installers-and-co-installers"></a>通过类安装程序和辅助安装程序修改注册表值


**注意**   通用或移动驱动程序包不支持本部分中介绍的功能。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

除非在某些情况下， *类安装* 程序和 *共同安装程序* 不得调用标准注册表函数来创建、更改或删除保留供操作系统使用的注册表值。

下面是此规则的例外情况：

-   必要时，类安装程序和共同安装程序可以使用标准注册表函数修改 **HKLM \\ 软件** 子树中的注册表值。

    **注意**   我们强烈建议类安装程序和共同安装程序将自定义设备属性保存为设备的*软件密钥*中的条目。

     

-   类安装程序和共同安装程序可以修改 [RunOnce 注册表项](runonce-registry-key.md)的值。 但是，此值必须仅由对 *Rundll32.exe*的调用组成。

    类安装程序和共同安装程序必须遵循有关如何在[INF 文件](overview-of-inf-files.md)中使用[RunOnce 注册表项](runonce-registry-key.md)的限制。 具体而言，此注册表项必须仅用于安装仅限软件的设备，这些设备使用软件设备枚举器 (SWENUM) 进行枚举。

-   当安装程序处理[**DIF_REGISTER_COINSTALLERS**](./dif-register-coinstallers.md)请求时，类安装程序和共同安装程序可以修改设备的*软件密钥*中的**CoInstallers32**和**EnumPropPages32**注册表值。

应遵循以下准则，以安全地修改类安装程序或共同安装程序的注册表值：

-   类安装程序和共同安装程序必须首先使用 [**SetupDiCreateDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdicreatedevregkeya) 或 [**SetupDiOpenDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdiopendevregkey) 来打开要修改的注册表项的句柄。 打开句柄后，类安装程序和共同安装程序可以使用标准注册表函数来修改注册表值。

-   类安装程序和共同安装程序不得对设备使用 **SetupDiDeleteDevRegKey** 或 *硬件密钥* 。 有关详细信息，请参阅 [删除设备的注册表项](deleting-the-registry-keys-of-a-device.md)。

有关标准注册表函数的详细信息，请参阅 [注册表函数](https://go.microsoft.com/fwlink/p/?linkid=194529)。

 


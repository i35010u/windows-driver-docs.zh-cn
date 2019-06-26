---
title: 通过类安装程序和辅助安装程序修改注册表值
description: 通过类安装程序和辅助安装程序修改注册表值
ms.assetid: 2D4B907A-622B-4b1b-A692-8E858F770F70
keywords:
- 注册表 WDK 设备安装，修改注册表值
- 注册表 WDK 设备安装，修改注册表值类安装程序
- 注册表 WDK 设备安装，修改注册表值，共同安装程序
- 类安装程序 WDK 设备安装，修改注册表值
- 共同安装程序 WDK 设备安装，修改注册表值
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a0213675ea93324f3207e2815ec4734e7252fd6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377643"
---
# <a name="modifying-registry-values-by-class-installers-and-co-installers"></a>通过类安装程序和辅助安装程序修改注册表值


**请注意**  通用或移动设备的驱动程序包中不支持在本部分中所述的功能。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

在某些情况下除外*类的安装程序*并*共同安装程序*必须调用要创建、 更改或删除保留以供的注册表值的标准注册表函数操作系统。

以下是此规则的例外情况：

-   在必要时，安装程序类和共同安装程序可以使用标准注册表函数来修改注册表值中的**HKLM\\软件**子树。

    **请注意**  我们强烈建议安装程序类共同安装程序，作为内设备的条目保存自定义设备属性*软件密钥*。

     

-   安装程序类和共同安装程序可以修改的值[RunOnce 注册表项](runonce-registry-key.md)。 但是，此值必须包含的仅调用*Rundll32.exe*。

    安装程序类和共同安装程序必须遵循有关如何使用限制[RunOnce 注册表项](runonce-registry-key.md)中[INF 文件](overview-of-inf-files.md)。 具体而言，此注册表项必须是仅用于枚举通过使用软件设备枚举器 (SWENUM) 的仅限软件的设备的安装。

-   安装程序类和共同安装程序可以修改**CoInstallers32**并**EnumPropPages32**中设备的注册表值*软件密钥*时安装程序处理[ **DIF_REGISTER_COINSTALLERS** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-register-coinstallers)请求。

以下指导原则后应执行以安全地修改注册表值类安装程序或共同安装程序：

-   安装程序类和共同安装程序必须首先使用[ **SetupDiCreateDevRegKey** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedevregkeya)或[ **SetupDiOpenDevRegKey** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)若要打开的句柄将修改注册表项。 打开句柄后，安装程序类和共同安装程序可以使用标准注册表函数来修改注册表值。

-   不能使用安装程序类和共同安装程序**SetupDiDeleteDevRegKey**或*硬件密钥*设备。 有关详细信息，请参阅[删除设备的注册表项](deleting-the-registry-keys-of-a-device.md)。

有关标准注册表函数的详细信息，请参阅[注册表函数](https://go.microsoft.com/fwlink/p/?linkid=194529)。

 

 






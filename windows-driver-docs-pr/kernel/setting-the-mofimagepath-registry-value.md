---
title: 设置 MofImagePath 注册表值
description: 设置 MofImagePath 注册表值
ms.assetid: b8c43cd3-d4f4-4f1e-b692-8005d845d64a
keywords:
- WMI WDK 内核，发布架构
- 发布 WMI 架构 WDK
- 发布 WDK WMI 架构
- MOF 文件 WDK WMI
- MofImagePath
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bb76d227a5bb056d0afab1d092ad614b7cea909
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385854"
---
# <a name="setting-the-mofimagepath-registry-value"></a>设置 MofImagePath 注册表值





可以通过在单独的文件，如的 DLL，包括已编译的 MOF 资源并设置发布的驱动程序的架构**MofImagePath**到该文件的路径在注册表中。 在这种方式中发布的架构可以无需重新编译该驱动程序更新。

若要在单独的文件中发布的驱动程序的架构：

1.  编译 MOF 文件中所述[编译的驱动程序的 MOF 文件](compiling-a-driver-s-mof-file.md)。

2.  为如的 DLL 文件中的资源包括编译的 MOF 文件。

3.  添加**MofImagePath**驱动程序的服务密钥下的注册表值。 例如，以下显示了名为的驱动程序的注册表值*DriverName*:

    ```cpp
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services
        \DriverName
            MofImagePath    "\SystemRoot\System32\Drivers\DriverNameMof.dll"
    ```

可以设置有关此密钥，驱动程序的 INF 文件，如下所示：

```cpp
; This is the Services section for the driver
[Driver_service_install_section]
AddReg=Driver_AddReg

; This is the Services AddReg section declared above.
[Driver_AddReg]
HKR,,MofImagePath,,DriverMof.dll 
```

请参阅[ **INF DDInstall.Services 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-services-section)并[ **INF AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)有关详细信息。

 

 





---
title: 用于加载部分已检验版本的启动参数
description: 用于加载部分已检验版本的启动参数
ms.assetid: 701a3258-d659-49a7-8e0d-52adc556a289
keywords:
- 部分已检验的版本启动选项 WDK
- 引导参数 WDK
- 启动入口参数 WDK
- 加载部分检查生成 WDK 启动选项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27993aaf78504ddf3ea490e98d52b0dea746b206
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344932"
---
#  <a name="boot-parameters-to-load-a-partial-checked-build"></a>用于加载部分已检验版本的启动参数


## <span id="ddk_boot_parameters_to_load_a_partial_checked_build_tools"></span><span id="DDK_BOOT_PARAMETERS_TO_LOAD_A_PARTIAL_CHECKED_BUILD_TOOLS"></span>


一个*部分已检验版本*包含的内核和 HAL 调试内部版本版本和操作系统的其余部分的免费版本。 有关详细信息，请参阅[安装只需检查操作系统和 HAL （适用于 Windows Vista 和更高版本）](installing-just-the-checked-operating-system-and-hal--for-windows-vist.md)。

### <a name="span-idconfiguringapartialcheckedbuildinwindowsvistaandlaterspanspan-idconfiguringapartialcheckedbuildinwindowsvistaandlaterspanconfiguring-a-partial-checked-build-in-windows"></a><span id="configuring_a_partial_checked_build_in_windows_vista_and_later"></span><span id="CONFIGURING_A_PARTIAL_CHECKED_BUILD_IN_WINDOWS_VISTA_AND_LATER"></span>在 Windows 中配置部分已检验的版本

若要配置部分检查生成使用[ **BCDedit /set** ](https://msdn.microsoft.com/library/windows/hardware/ff542202)命令并**内核**并**hal**选项。

以下命令将配置为使用的内核和硬件抽象层 (HAL) 付费版本的启动项。

```
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} kernel ntoskrnl.chk
```

```
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} hal halacpi.chk
```

若要查看命令的结果，请键入**bcdedit /enum**。 **/Enum**选项可列出所有启动项。 已修改为使用的内核和 HAL 付费版本的启动项目也在配置用于内核调试通过串行连接。

```
## Windows Boot Loader
-------------------
identifier              {18b123cd-2bf6-11db-bfae-00e018e2b8db}
device                  partition=C:
path                    \Windows\system32\winload.exe
description             PartialCheckedBuild
locale                  en-US
inherit                 {bootloadersettings}
debugtype               serial
debugport               1
baudrate                115200
osdevice                partition=C:
systemroot              \Windows
kernel                  ntoskrnl.chk
hal                     halacpi.chk
resumeobject            {d7094401-2641-11db-baba-00e018e2b8db}
nx                      OptIn
debug                   Yes
```

 

 






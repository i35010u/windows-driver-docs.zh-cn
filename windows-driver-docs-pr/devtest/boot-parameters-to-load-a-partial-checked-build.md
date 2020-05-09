---
title: 用于加载部分已检验版本的启动参数
description: 用于加载部分已检验版本的启动参数
ms.assetid: 701a3258-d659-49a7-8e0d-52adc556a289
keywords:
- 部分检查的生成启动选项 WDK
- 启动参数 WDK
- 启动项参数 WDK
- 加载部分检查的生成 WDK 启动选项
ms.date: 05/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: fa6ca83044bbf0b80cca960f693dc680b358eb81
ms.sourcegitcommit: 076f9cd83313f6d8ab5688340f05bde7e8fbb8ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2020
ms.locfileid: "82999026"
---
#  <a name="boot-parameters-to-load-a-partial-checked-build"></a>用于加载部分已检验版本的启动参数

## <span id="ddk_boot_parameters_to_load_a_partial_checked_build_tools"></span><span id="DDK_BOOT_PARAMETERS_TO_LOAD_A_PARTIAL_CHECKED_BUILD_TOOLS"></span>

*部分检查的生成*包含内核和 HAL 的已检查内部版本以及操作系统剩余部分的免费版本。 有关详细信息，请参阅[仅安装已检查的操作系统和 HAL （适用于 Windows Vista 和更高版本）](installing-just-the-checked-operating-system-and-hal--for-windows-vist.md)。

> [!NOTE]
> 在 Windows 10 版本1803之前，已检查的生成在较早版本的 Windows 上可用。
> 使用驱动程序验证程序和 GFlags 等工具检查驱动程序代码。


### <a name="span-idconfiguring_a_partial_checked_build_in_windows_vista_and_laterspanspan-idconfiguring_a_partial_checked_build_in_windows_vista_and_laterspanconfiguring-a-partial-checked-build-in-windows"></a><span id="configuring_a_partial_checked_build_in_windows_vista_and_later"></span><span id="CONFIGURING_A_PARTIAL_CHECKED_BUILD_IN_WINDOWS_VISTA_AND_LATER"></span>在 Windows 中配置部分检查的生成

若要配置部分检查的生成，请使用[**BCDedit/set**](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)命令和**内核**和**hal**选项。

以下命令将配置启动项以使用内核和硬件抽象层（HAL）的已检查版本。

```console
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} kernel ntoskrnl.chk
```

```console
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} hal halacpi.chk
```

若要查看命令的结果，请键入**bcdedit/enum**。 **/Enum**选项列出所有启动项。 已修改为使用所选内核和 HAL 版本的启动条目也已配置为通过串行连接进行内核调试。

```console
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

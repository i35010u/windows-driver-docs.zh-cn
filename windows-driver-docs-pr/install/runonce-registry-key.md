---
title: RunOnce 注册表项
description: RunOnce 注册表项
ms.assetid: dbeb7be7-4d38-49e2-944c-ea95d9914ebe
keywords:
- RunOnce 注册表项
- 注册表 WDK 设备安装
- 设备安装 WDK，注册表
- 安装设备 WDK、注册表
- 设备设置 WDK 设备安装，注册表
- 驱动程序注册表 RunOnce 密钥 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb7ccdf878e725806c74d646e3b31bc54caa45c1
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732715"
---
# <a name="runonce-registry-key"></a>RunOnce 注册表项





所有版本的 Windows 都支持一个注册表项 **RunOnce**，此注册表项可用于指定系统将执行一次然后删除的命令。

在 Windows 8 和 Windows 8.1 中，在设备安装过程中会处理用于安装仅软件 SWENUM 设备的 **RunOnce** 条目。 其他 **runonce** 项将添加到 **runonce** 项。 它们将在系统下一次处理 **RunOnce** 密钥时应用。 设备安装不会强制系统处理 **RunOnce** 条目。

在 Windows 7 和以前的版本中，安装设备后，Windows 会立即执行存储在 **RunOnce** 项下的命令，然后删除该密钥。 此外，当系统每次启动时，它会执行存储在 **RunOnce** 项下的命令，然后删除该密钥。 因此，如果将命令放在 **RunOnce** 项下面，则无法轻松地预测执行时间。

安装设备后，Windows 会立即执行存储在 **RunOnce** 项下的命令，然后删除该密钥。 此外，当系统每次启动时，它会执行存储在 **RunOnce** 项下的命令，然后删除该密钥。 因此，如果将命令放在 **RunOnce** 项下面，则无法轻松地预测执行时间。

对于设备安装，可以通过使用通过[**INF AddReg 指令**](inf-addreg-directive.md)指定的 "*添加注册表" 部分*来创建**RunOnce**注册表项。 每个 " *添加注册表" 部分* 都具有以下语法：

`reg-root, [subkey], [value-entry-name], [flags], [value]`

**RunOnce**注册表项的注册表根 (*reg*) 和子键值如下所示：

**HKLM，"Software \\ Microsoft \\ Windows \\ CurrentVersion \\ RunOnce"**

在**RunOnce**注册表项中省略了*值输入名称*字符串。 项的类型（由 *flags* 值指示）必须是 [REG_SZ](/windows/desktop/SysInfo/registry-value-types) (*标志* 值 0x00000000) 或 [REG_EXPAND_SZ](/windows/desktop/SysInfo/registry-value-types) (*flags* 值为 0x00010000) 。 对于 (默认) [REG_SZ](/windows/desktop/SysInfo/registry-value-types) 类型的条目，可以省略 *Flags* 值。

**RunOnce**键中的*值*参数指定要执行的命令。 此参数是采用以下格式的带引号的字符串：

```cpp
Rundll32[.exe] DllName,EntryPoint[Arguments]
```

默认情况下，将在执行指定命令后删除 **RunOnce** 密钥。 你可以使用感叹号 (！ ) 为 **RunOnce** *键值参数加* 上前缀，以便在命令成功运行之前延迟删除密钥。 如果指定的命令失败， **则该命令** 将仍会被删除，并且在系统下一次启动时不会执行该命令。

另外，默认情况下，当系统在安全模式下启动时，将忽略 **RunOnce** 密钥。 可以在**RunOnce**密钥的*值*参数前面加上一个星号 (\*) 以强制在安全模式下执行命令。

创建 *值* 字符串条目时，请考虑以下准则：

-   *Rundll32.exe* 可以在其 *.exe* 文件扩展名的情况下出现。

-   *DllName* 是 DLL 或可执行映像的完整路径。 除必需的终止逗号外，表达式不得以其他方式包含任何逗号。 如果未提供文件扩展名，则默认扩展名为 *.dll*。

-   *EntryPoint* 是 *DLLNAME*指定的 DLL 中入口点的名称。

-   *参数* 是一个可选的子字符串，其中包含必须传递到指定 DLL 的所有参数。

-   只有一个空格必须将 *入口点* 字符串与 *参数* substring 分隔开来。

下面的代码示例演示了在**RunOnce**键下存储命令及其参数的 "*添加注册表" 部分*条目：

```cpp
;; WDMAud swenum install

HKLM,%RunOnce%,"WDM_WDMAUD",,\
"rundll32.exe streamci.dll,StreamingDeviceSetup %WDM_WDMAUD.DeviceId%,%KSNAME_Filter%,%KSCATEGORY_WDMAUD%,%17%\WDMAUDIO.inf,WDM_WDMAUD.Interface.Install"

[Strings]
RunOnce = "SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce"
WDM_WDMAUD.DeviceId = "{CD171DE3-69E5-11D2-B56D-0000F8754380}"
KSNAME_Filter = "{9B365890-165F-11D0-A195-0020AFD156E4}"
KSCATEGORY_WDMAUD = "{3E227E76-690D-11D2-8161-0000F8775BF1}"
```

使用 **RunOnce** 注册表项进行设备安装时，下列规则适用：

-   这些注册表项必须仅用于 SWENUM （软件设备枚举器）所枚举的仅限软件的设备的安装。

-   **RunOnce** 密钥只能由对 *Rundll32.exe*的调用组成。 否则，WHQL 不会对 [驱动程序包](driver-packages.md)进行数字签名。

-   要执行的代码不得提示用户输入。

-   服务器端安装在系统上下文中执行。 出于此原因，必须确定要执行的代码不包含任何安全漏洞，并且该文件权限会阻止对代码进行恶意修改。

-   从 Windows Vista 开始，如果没有管理员权限的用户登录到系统，则系统不会执行 **RunOnce** 密钥指定的命令。 在系统重新启动后，这可能会导致安装不完整或已损坏。

    在 *设备安装应用程序* 创建 **RunOnce** 条目之前，它会通知当前用户具有管理员权限的用户必须在系统重新启动后登录。

    有关详细信息，请参阅 [开发在 Windows Vista 上登录时运行的应用程序](/previous-versions/bb325654(v=msdn.10))。


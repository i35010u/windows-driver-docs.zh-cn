---
title: RunOnce 注册表项
description: RunOnce 注册表项
ms.assetid: dbeb7be7-4d38-49e2-944c-ea95d9914ebe
keywords:
- RunOnce 注册表项
- 注册表 WDK 设备安装
- 设备安装 WDK、 注册表
- 安装设备 WDK、 注册表
- 设备安装程序 WDK 设备安装、 注册表
- 驱动程序注册表 RunOnce 密钥 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf05620ed9ad77c9f0113c6cb0e31bf525af3544
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382920"
---
# <a name="runonce-registry-key"></a>RunOnce 注册表项





所有版本的 Windows 都支持注册表项， **RunOnce**，这可用于指定系统将执行其中一个命令的时间，然后删除。

在 Windows 8 和 Windows 8.1 **RunOnce**在设备安装过程中处理的纯软件 SWENUM 设备安装的项。 其他**RunOnce**项添加到**RunOnce**密钥。 应用下一次系统处理这些**RunOnce**密钥。 设备安装不会强制系统来处理**RunOnce**条目。

在 Windows 7 和早期版本中，立即安装设备后，Windows 执行的命令存储在下**RunOnce**键，然后删除的项。 此外，每次系统启动时，它执行存储在下面的命令**RunOnce**键，然后删除的项。 因此，如果在命令放**RunOnce**密钥，您不能轻松地预测其执行时间。

Windows 安装设备后，执行存储在该命令立即**RunOnce**键，然后删除的项。 此外，每次系统启动时，它执行存储在下面的命令**RunOnce**键，然后删除的项。 因此，如果在命令放**RunOnce**密钥，您不能轻松地预测其执行时间。

对于设备安装**RunOnce**可以通过创建注册表项*添加注册表部分*，这通过指定[ **INF AddReg 指令**](inf-addreg-directive.md). 每个*添加注册表部分*具有以下语法：

`reg-root, [subkey], [value-entry-name], [flags], [value]`

注册表根目录 (*reg 根*) 和子项的值**RunOnce**注册表项如下所示：

**HKLM, "Software\\Microsoft\\Windows\\CurrentVersion\\RunOnce"**

*值的条目名称*字符串中省略**RunOnce**注册表项。 由指示的项的类型*标志*值，必须是[REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types) (*标志*0x00000000 的值) 或[REG_EXPAND_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)(*标志*0x00010000 值)。 类型的条目[REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types) （默认值），*标志*可以省略值。

*值*中的参数**RunOnce**密钥指定要执行的命令。 此参数是带引号的字符串具有以下格式：

```cpp
Rundll32[.exe] DllName,EntryPoint[Arguments]
```

默认情况下**RunOnce**执行指定的命令后删除密钥。 您可以前缀**RunOnce**密钥*值*感叹号 （！），该命令成功运行后，将延迟的键，直到删除参数。 如果没有感叹号前缀，如果指定的命令失败， **RunOnce**密钥仍将被删除，该命令将不会执行在系统启动下一次。

此外，默认情况下， **RunOnce**系统开始在安全模式下，密钥将被忽略。 *值*的参数**RunOnce**密钥可以带星号前缀 (\*) 若要强制甚至在安全模式下执行的命令。

在创建时，请考虑以下准则*值*字符串条目：

-   *Rundll32*无论是否可以显示其 *.exe*文件扩展名。

-   *Dll 名称*是 DLL 或可执行映像的完整路径。 除了需要终止逗号表达式不得否则包含所有逗号。 如果提供无文件扩展名，则默认扩展名是 *.dll*。

-   *EntryPoint*中所指示的 DLL 的入口点的名称*DllName*。

-   *参数*是可选的子字符串，其中包含任何参数，必须传递给指定的 DLL。

-   必须只有一个空格来分隔*EntryPoint*中的字符串*自变量*子字符串。

下面的代码示例演示*添加注册表部分*条目，用于存储命令，并在其自变量**RunOnce**密钥：

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

使用时，以下规则适用**RunOnce**对于设备安装的注册表项：

-   这些注册表项必须仅用于通过 SWENUM，软件设备枚举器枚举的仅限软件的设备的安装。

-   **RunOnce**密钥必须仅包含对*Rundll32.exe*。 否则，WHQL 将未进行数字签名[驱动程序包](driver-packages.md)。

-   若要执行的代码必须提示用户输入。

-   在系统上下文中执行服务器端的安装。 出于此原因，您必须确保要执行的代码包含任何安全漏洞和文件权限防止代码的恶意修改。

-   从 Windows Vista 开始，系统将不会执行指定的命令**RunOnce**密钥如果没有管理员权限的用户登录到系统。 这可能会导致到不完整或已损坏的安装以下系统重新启动。

    之前*设备安装应用程序*创建**RunOnce**条目，它会通知当前在系统重新启动后，具有管理员权限的用户必须登录的用户。

    有关详细信息，请参阅[开发应用程序在 Windows Vista 上运行的登录](https://go.microsoft.com/fwlink/p/?linkid=133224)。

 

 






---
title: 在开发和测试期间安装未签名驱动程序
description: 在开发和测试期间安装未签名驱动程序
keywords:
- 驱动程序签名 WDK，未签名的驱动程序
- 对驱动程序进行签名 WDK，未签名的驱动程序
- 数字签名 WDK，未签名的驱动程序
- 签名 WDK，未签名的驱动程序
- 测试签名驱动程序 WDK，未签名的驱动程序
- 未签名的驱动程序安装 WDK 驱动程序签名
- 内核调试器 WDK 驱动程序签名
- 内核模式驱动程序签名 WDK
- F8 密钥 WDK drvier 签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d719ad760ebd699f1719819bcf3eea3409682b8d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794895"
---
# <a name="installing-an-unsigned-driver-during-development-and-test"></a>在开发和测试期间安装未签名驱动程序


默认情况下，仅当内核可以验证驱动程序签名时，Windows Vista 和更高版本的 windows 的64位版本才会加载内核模式驱动程序。 但是，在早期的驱动程序开发和非自动测试过程中，可以禁用此默认行为。 开发人员可以使用以下机制之一来暂时禁用有效驱动程序签名的加载时间强制。 但是，若要完全自动测试即插即用 (PnP) 安装的驱动程序，则必须对该驱动程序的 [编录文件](catalog-files.md) 进行签名。 需要对驱动程序进行签名的原因是 Windows Vista 和更高版本的 Windows 将为需要系统管理员授权安装驱动程序的无符号驱动程序显示 "驱动程序签名" 对话框，这可能会阻止没有必要权限的用户安装驱动程序和使用设备。 无法在 Windows Vista 和更高版本的 Windows 上禁用此 PnP 驱动程序安装行为。

### <a name="use-the-f8-advanced-boot-option"></a>**使用 "F8 高级启动" 选项**

Windows Vista 和更高版本的 Windows 支持 F8 高级启动选项--"禁用驱动程序签名强制"--该选项仅对当前系统会话禁用内核模式驱动程序的加载时签名强制。 此设置不会在系统重新启动期间保持。

### <a name="attach-a-kernel-debugger-to-disable-signature-verification"></a><a href="" id="attach-a-kernel-debugger-to-disable-signature-verification"></a> 附加内核调试器以禁用签名验证

将活动内核调试器附加到开发或测试计算机会禁用内核模式驱动程序的加载时签名强制。 若要使用此调试配置，请将调试计算机附加到开发或测试计算机，然后通过运行以下命令在开发或测试计算机上启用内核调试：

```cpp
bcdedit -debug on
```

若要使用 BCDEdit，用户必须是系统上 Administrators 组的成员，并从提升的命令提示符运行该命令。 若要打开提升的命令提示符窗口，请创建 *Cmd.exe* 的桌面快捷方式，选择并按住 (或右键单击该快捷方式) ，然后选择 " **以管理员身份运行**"。

### <a name="enforcing-kernel-mode-signature-verification-in-kernel-debugging-mode"></a><a href="" id="enforcing-kernel-mode-signature-verification-in-kernel-debugging-mode"></a> 在内核调试模式下强制 Kernel-Mode 签名验证

但是，在某些情况下，开发人员可能需要附加内核调试器，还需要维护加载时签名的执行。 例如，当驱动程序堆栈具有未签名的驱动程序 (例如无法加载的筛选器驱动程序) 时，可能会使整个堆栈无效。 由于附加调试器允许加载未签名的驱动程序，因此，一旦附加调试器，问题就会消失。 调试此类问题可能比较困难。

为了便于调试此类问题， [内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md) 支持以下注册表值：

```cpp
HKLM\SYSTEM\CurrentControlSet\Control\CI\DebugFlags
```

此注册表值的类型为 [REG_DWORD](/windows/desktop/SysInfo/registry-value-types)，可以根据一个或多个以下标志的按位 "或" 指定值：

<a href="" id="0x00000001"></a>**0x00000001**  
此标志值将内核配置为在驱动程序未签名时中断到调试器。 然后，开发人员或测试人员可以通过在调试器提示符下输入 **g** 来选择加载未签名的驱动程序。

<a href="" id="0x00000010"></a>**0x00000010**  
此标志值将内核配置为忽略调试器的状态，并始终阻止未签名的驱动程序加载。

如果注册表中不存在此注册表值，或者其值不基于前面所述的标志，则内核将始终在内核调试模式下加载驱动程序，而不管驱动程序是否已签名。

**注意**  默认情况下，注册表中不存在此注册表值。 必须创建值才能调试内核模式签名验证。

 

 


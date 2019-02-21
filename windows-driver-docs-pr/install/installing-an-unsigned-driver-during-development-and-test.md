---
title: 在开发和测试期间安装未签名的驱动程序
description: 在开发和测试期间安装未签名的驱动程序
ms.assetid: b7b08d5a-40cf-498f-8645-6b02d803f62f
keywords:
- 驱动程序签名 WDK，未签名驱动程序
- 签署驱动程序 WDK，未签名驱动程序
- 数字签名 WDK，未签名驱动程序
- 签名 WDK，未签名驱动程序
- 测试签名驱动程序 WDK，未签名驱动程序
- 未签名驱动程序安装 WDK 驱动程序签名
- 内核调试器 WDK 驱动程序签名
- 内核模式驱动程序签名 WDK
- F8 键 WDK 它签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03d34534f308fc97938ac456eb8948f95ab250e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546888"
---
# <a name="installing-an-unsigned-driver-during-development-and-test"></a>在开发和测试期间安装未签名的驱动程序


默认情况下，64 位版本的 Windows Vista 和更高版本的 Windows 将加载的内核模式驱动程序仅当内核可以验证驱动程序签名。 但是，在早期驱动程序开发期间以及非自动测试到已禁用此默认行为。 开发人员可以使用以下机制之一来暂时禁用加载时强制实施有效的驱动程序签名。 但是，若要完全自动执行测试的情况下插即用 (PnP) 安装的驱动程序[编录文件](catalog-files.md)必须签名的驱动程序。 签名驱动程序是必需的因为 Windows Vista 和更高版本的 Windows 显示驱动程序签名需要系统管理员进行授权的驱动程序安装的未签名驱动程序的对话框中，这可能会导致无需任何用户从安装驱动程序以及使用该设备的必要权限。 不能在 Windows Vista 和更高版本的 Windows 上禁用此即插即用驱动程序安装行为。

### <a name="use-the-f8-advanced-boot-option"></a>**使用 F8 高级启动选项**

Windows Vista 和更高版本的 Windows 支持的 F8 高级启动选项-"禁用强制驱动程序签名"-禁用强制内核模式驱动程序的加载时间签名仅为当前的系统会话。 在系统重启后不保留此设置。

### <a href="" id="attach-a-kernel-debugger-to-disable-signature-verification"></a> 附加内核调试器来禁用签名验证

将活动内核调试程序附加到开发或测试计算机禁用内核模式驱动程序的强制加载时签名。 若要使用此调试配置，将调试的计算机附加到需要开发或测试计算机，并启用内核调试上开发或通过运行以下命令测试计算机：

```cpp
bcdedit -debug on
```

若要使用 BCDEdit，用户必须是系统上的 Administrators 组的成员并从提升的命令提示符运行命令。 若要打开提升的命令提示符窗口，请创建桌面快捷方式*Cmd.exe*，右键单击该快捷方式，然后选择**以管理员身份运行**。

### <a href="" id="enforcing-kernel-mode-signature-verification-in-kernel-debugging-mode"></a> 强制在调试模式下的内核的内核模式签名验证

但是，有些情况下在其中一名开发人员可能需要附加，内核调试器，但还需要维护强制加载时签名。 例如，当驱动程序堆栈 （例如筛选器驱动程序） 无法加载未签名驱动程序时，这可能会使整个堆栈。 由于附加调试程序允许加载未签名驱动程序，将出现此问题已附加调试器时，就立即消失。 调试此类问题可能很难。

为了便于调试此类问题[内核模式代码签署策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)支持以下注册表值：

```cpp
HKLM\SYSTEM\CurrentControlSet\Control\CI\DebugFlags
```

此注册表值为类型[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)，并且可以分配基于一个或多个下列标志的按位 OR 的值：

<a href="" id="0x00000001"></a>**0x00000001**  
此标志值配置中断调试器，如果驱动程序是无符号的内核。 开发人员或测试人员然后可以选择要加载未签名的驱动程序通过输入**g**调试器提示符处。

<a href="" id="0x00000010"></a>**0x00000010**  
此标志值将配置为忽略调试器存在并将始终阻止加载未签名驱动程序的内核。

如果此注册表值在注册表中不存在或不基于前面所述的标志的值，内核将始终加载内核调试模式，而无论是否签名驱动程序中的驱动程序。

**请注意**  此注册表值中不存在注册表默认情况下。 若要调试内核模式签名验证，必须创建值。

 

 

 






---
title: WDK 已知问题
description: 'Windows 驱动程序工具包的已发行版本的已知问题列表 (WDK) '
keywords:
- Windows 驱动程序工具包 (WDK)
- WDK
- 驱动程序
- 已知问题
ms.date: 12/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: c9e09f0edd48da6423194e21fe206a138627311b
ms.sourcegitcommit: af11b2eadb883846583e541ae13eb1d4e0dec220
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/18/2020
ms.locfileid: "97691813"
---
# <a name="windows-driver-kit-wdk-known-issues"></a>Windows 驱动程序工具包 (WDK) 已知问题

本主题详细介绍了与 WDK 有关的已知问题。

## <a name="wdk-for-windows-10-version-2004"></a>适用于 Windows 10 版本 2004 的 WDK

### <a name="issue-in-exallocatepoolzero-exallocatepoolquotazero-and-exallocatepoolpriorityzero-functions-fixed"></a>修复了 ExAllocatePoolZero、ExAllocatePoolQuotaZero 和 ExAllocatePoolPriorityZero 函数中的问题

在5月2020， [OSR](https://www.osr.com/) 发现新的对池分配的下层支持发生了一个问题，该问题可能导致在运行 Windows 10 1909 版的系统上分配未初始化为零。 现在，已使用适用于 Windows 10 的 WDK （版本2004）和企业版 WDK (EWDK) 在12月16日版本2004上对此进行了安全更新。 Microsoft 利用了安全刷新并更新了 EWDK 以包含 Visual Studio 生成工具16.7。 Microsoft 建议所有驱动程序开发人员卸载原始 SDK 和 WDK (版本 2004) 并安装 refresh SDK 和 WDK 或 EWDK。

为了确保已有完整的安全解决方案，在11月版本1909中发布了一个操作系统修补程序，因此，如果有一个驱动程序在安全问题的情况下创建，则操作系统将受到保护。

除了下载更新后的 WDK/EWDK，Microsoft 建议所有驱动程序都将所有内核分配切换为使用新的池零位调整 DDIs，默认情况下返回零内存。 这会增加驱动程序的安全性和可靠性。 为了帮助进行此转换，Microsoft 创建了静态驱动程序验证程序规则，该规则在预览版 Windows 10 WDK 20236 及更高版本中可用。 此规则将标识驱动程序源代码中的所有实例，其中使用旧的池分配 DDIs，并建议使用新的、更安全的等效 DDI 替换它们。 此规则适用于 WDM、WDF 和基于 NDIS 的驱动程序。

### <a name="installing-wdk-no-longer-enables-spectre-mitigations-for-all-c-projects-as-seen-in-wdk-1903"></a>安装 WDK 不再为所有 c + + 项目启用 Spectre 缓解功能，如 WDK 1903 中所示

尽管在默认情况下，对于所有驱动程序，WDK 安装都将启用 Spectre 缓解功能，但不会再对所有 c + + 项目启用它们。

### <a name="error-a-wdk-corresponding-to-target-100190410-was-not-found"></a>"找不到与目标 ' 10.0.19041.0 ' 对应的 WDK" 错误。

使用 WDK 10.0.19041.0 选择 [Windows SDK 版本] 到 "10.0 (最新安装的版本) " 时，即使安装了 SDK 版本也会导致 "找不到与目标版本 ' 10.0.19041.0 ' 对应的 WDK" 错误。

**解决方法：** 在驱动程序项目的 "属性" 页中 (配置属性 >常规) 将 Windows SDK 版本设置为 $ (LatestTargetPlatformVersion) 。 如果此选项不可用于选择，则选择 " **从父级或项目默认值继承**" 选项。

### <a name="ewdk-and-sdv-running-on-server-have-net-requirements"></a>服务器上运行的 EWDK 和 SDV 具有 .NET 要求

从 EWDK 运行静态驱动程序验证程序需要 .Net Framework 4.7.2。 根据您的系统上的 Windows 版本，可能会安装 .NET、安装但需要启用它，或者可能没有安装。 有关安装的 .NET 版本或 .NET 安装状态的详细信息，请查看 [.NET Framework 版本和依赖项](/dotnet/framework/migration-guide/versions-and-dependencies)。

### <a name="dvl-generation-fails-with-systemiofilenotfoundexception"></a>DVL 生成失败，出现 System.io.filenotfoundexception

尝试创建驱动程序验证日志 (DVL) 时，将显示以下错误：

```console
Unhandled Exception: System.IO.FileNotFoundException: 
Could not load file or assembly 
'System.Runtime, Version=4.2.1.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' 
or one of its dependencies. 
The system cannot find the file specified.
```

这种情况可能发生在命令行和 GUI 环境中。  此问题已在未来版本的 WDK 中解决，可在 [Windows 预览体验](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)版中查看。 遗憾的是，当前版本没有解决方法。

### <a name="sdv-fails-in-the-ewdk-if-vs-is-not-installed"></a>如果未安装 VS，则 EWDK 中的 SDV 失败

SDV 依赖于 Visual Studio 中 VCRUNTIME140D.dll。  因此，在未安装 VS 的计算机上运行 EWDK 将会失败。  在计算机上安装 Visual Studio，以解决此问题。

### <a name="driver-verifier-does-not-get-enableddisabled-when-using-wdk-test-explorer"></a>使用 WDK 测试资源管理器时，驱动程序验证程序不启用/禁用

当使用 WDK 测试资源管理器运行设备基础测试时，驱动程序验证器不会启用/禁用。

**解决方法：** 在客户端计算机上，根据这些说明手动启用/禁用驱动程序验证程序。

### <a name="wdk-side-by-side-installations-of-windows-10-version-2004-and-wdk-windows-10-version-1903-or-version-1803"></a>WDK 并行安装 Windows 10 版本2004和 WDK Windows 10，版本1903或版本1803

在同一台计算机上安装两个版本的工具包时，"部署驱动程序" 功能不适用于较旧版本。

**解决方法：** 如果需要部署驱动程序功能，请在单独的计算机上使用1803。

### <a name="windows-device-testing-framework-wdtf-tests-now-only-run-on-systems-with-matching-windows-10-versions-as-the-wdk"></a>Windows 设备测试框架 (WDTF) 测试现在只能在具有与 WDK 相同的 Windows 10 版本的系统上运行

在适用于 Windows 10 的 WDK 版本1809中，对 WDTF 进行了更改，以便支持此版本的 Windows 10，版本1809。 这样做的效果是，WDTF 将不再在下级 OS 上运行。 此更改继续于适用于 Windows 10 版本2004的 WDK。

#### <a name="alterative-for-down-level-testing"></a>用于下级测试的另

Windows 10 版本1803中的 WDTF 测试可在以前的 Windows 版本上运行。

### <a name="apivalidator"></a>APIValidator

在 x86 的计算机上，APIValidator 无法针对 x64 二进制文件运行。 如果在 x86 计算机上构建 x64 驱动程序 APIValidator 应关闭。

**解决方法：**

1. 请参阅驱动程序解决方案的属性页。

2. 选择 **APIValidator**，然后选择 " **常规**"，然后将 " **运行 APIValidator** **" 从 "是"** 更改为 " **否**"。

### <a name="wdk-running-on-windows-7-systems-requires-kb-3033929"></a>在 Windows 7 系统上运行的 WDK 需要 KB 3033929

在运行 Windows 7 的系统上安装 WDK 之前，必须先安装 Microsoft Security 公告 3033929 (KB3033929) 。  可从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=46148)下载 KB3033929。

### <a name="installing-the-wdk-generates-an-error-from-visual-studio-that-the-add-in-component-is-already-installed"></a>安装 WDK 会从 Visual Studio 生成一个错误，指出已安装了外接程序组件

如果已卸载 WDK 但未卸载适用于 Visual Studio 的 WDK 驱动程序扩展，则会出现此错误消息。

**解决方法：** 在 Visual Studio 中，单击 " **扩展** " 下拉菜单，选择 " **管理扩展**"，选择 **Windows 驱动程序工具包**，然后单击 " **卸载**"。

## <a name="faq"></a>常见问题解答

### <a name="how-do-i-tell-if-the-wdk-or-ewdk-versions-i-have-contains-the-fix-for-the-zeroing-of-pool-allocations"></a>如何实现判断我是否包含用于池分配的零位调整的 WDK 或 EWDK 版本？

在 " **系统设置** " 中，请参阅 " **添加或删除程序**"，搜索 **Windows 驱动程序工具包** 并记下版本。 适用于 Windows 10 的原始 WDK 版本2004具有10.0.19041.1 版本，并且在启动 EWDK 环境后，EWDK 的刷新 WDK 版本10.0.19041.685 为，并在启动环境后查看命令窗口的标题。 刷新后的版本将包含 **vb_release_svc_prod1。 19041.685**。 此外，查看环境变量时， **BuildLab** 变量应显示 **vb_release_svc_prod1. 19041.685**。  

### <a name="the-windows-software-development-kit-sdk-was-also-refreshed-is-this-needed-as-well"></a>还刷新了 Windows 软件开发工具包 (SDK) ，是否需要这样做？

不，但刷新的 Windows 软件开发工具包 (SDK) 包含对 onecore 的修补程序，这可能很好。 此外，将 SDK 和 WDK 保持一致通常是个好主意。

### <a name="if-i-already-have-the-wdk-for-windows-10-version-2004-installed-do-i-need-to-uninstall-it-before-installing-the-refreshed-version"></a>如果我已安装了适用于 Windows 10 的 WDK 2004 版，则在安装刷新版本之前，是否需要卸载它？

如果您的原始 2004 SDK 和 WDK 已卸载，并且安装了安全刷新 SDK 和 WDK，则强烈建议您这样做。 也就是说，如果刷新后的 WDK 安装在原始 WDK 的顶部，则刷新后的版本将覆盖原版本。 注意：在此方案中，这两个版本都将列出。

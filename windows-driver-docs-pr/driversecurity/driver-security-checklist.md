---
title: 驱动程序安全清单
description: 本文提供驱动程序开发人员的驱动程序安全清单。
ms.assetid: 25375E02-FCA1-4E94-8D9A-AA396C909278
ms.date: 04/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: 18c3e78adf67644de5cdfd8c434cf36d4ba78739
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371455"
---
# <a name="driver-security-checklist"></a>驱动程序安全清单

本文提供了驱动程序开发人员以帮助减少驱动程序遭到入侵的风险的驱动程序安全清单。

## <a name="span-iddriversecurityoverviewspanspan-iddriversecurityoverviewspanspan-iddriversecurityoverviewspandriver-security-overview"></a><span id="Driver_Security_Overview"></span><span id="driver_security_overview"></span><span id="DRIVER_SECURITY_OVERVIEW"></span>驱动程序安全概述

安全漏洞是允许攻击者导致驱动程序无法正常工作的方式，它会导致系统崩溃或变得不可用任何缺陷。 此外，驱动程序代码中的漏洞可以允许攻击者有权创建可能危及整个 OS 内核。 大多数开发人员工作时在其驱动程序，其重点是获取驱动程序才能正常工作，而不是在是否尝试恶意攻击者利用其代码中的漏洞。

发布一个驱动程序后，但是，攻击者可以尝试探测，确定安全漏洞。 为了最小化此类漏洞的可能性，开发人员必须在设计和实施阶段考虑这些问题。 目标是以发布该驱动程序之前消除所有已知的安全缺陷。

创建更安全的驱动程序需要系统架构师 （有意识地从考虑该驱动程序的潜在威胁），协助开发人员实现代码 （采用防御方式进行编码可攻击的源的常见操作） 和测试团队 （主动尝试查找漏洞和漏洞）。 通过正确地协调所有这些活动，极大地增强的驱动程序的安全性。

除了避免受到攻击的驱动程序与相关的问题，很多步骤所述，例如更精确地使用内核内存会增加您的驱动程序的可靠性。 这将减少支持成本并提高客户满意度和你的产品。 完成以下清单中的任务将有助于实现这些目标。

**安全核对清单：***完成安全任务，每个主题中所述。*

![空的复选框](images/checkbox.png)[确认所需的内核驱动程序](#confirmkernel)

![空的复选框](images/checkbox.png)[使用驱动程序框架](#confirmkernel)

![空的复选框](images/checkbox.png)[控制对软件仅驱动程序的访问](#controlsoftwareonly)

![空的复选框](images/checkbox.png)[进行非生产标记测试驱动程序代码](#donotproductionsign) 

![空的复选框](images/checkbox.png)[执行威胁分析](#threatanalysis)

![空的复选框](images/checkbox.png)[按照驱动程序安全编码准则](#driversecuritycodepractices)

![空的复选框](images/checkbox.png)[验证 Device Guard 兼容性](#dgc)

![空的复选框](images/checkbox.png)[遵循技术特定代码的最佳做法](#technologyspecificcodepractices)

![空的复选框](images/checkbox.png)[执行对等代码评审](#peercodereview)

![空的复选框](images/checkbox.png)[管理驱动程序的访问控制](#managingdriveraccesscontrol)

![空的复选框](images/checkbox.png)[增强设备安装的安全性](#enhancedeviceinstallationsecurity)

![空的复选框](images/checkbox.png)[执行正确的版本驱动程序签名](#releasedriversigning)

![空的复选框](images/checkbox.png)[使用 Visual Studio 中的代码分析来调查驱动程序的安全性](#use-code-analysis)

![空的复选框](images/checkbox.png)[检查的漏洞使用 Static Driver Verifier](#sdv)

![空的复选框](images/checkbox.png)[检查 Binscope 二进制分析工具的代码](#binscope)

![空的复选框](images/checkbox.png)[使用代码验证工具](#codevalidationtools)

![空的复选框](images/checkbox.png)[查看调试器技术和扩展](#debugger)

![空的复选框](images/checkbox.png)[查看安全编码资源](#securecodingresources)

[关键结论的摘要](#keytakeaways)

## <a name="span-idconfirmkernelspanconfirm-that-a-kernel-driver-is-required"></a><span id="confirmkernel"></span>确认所需的内核驱动程序

**安全核对清单项\#1:***确认内核驱动程序，则需要和较低的风险方法，例如，Windows 服务或应用程序，不是更好的选择。*

驱动程序位于 Windows 内核中，并在内核中执行时遇到问题公开整个操作系统。 如果任何其他选项可用，它有可能将会较低成本，并且具有较少关联的风险比创建新的内核驱动程序。
有关使用内置的 Windows 驱动程序的详细信息，请参阅[需要编写驱动程序？](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/do-you-need-to-write-a-driver-)。

有关使用后台任务的信息，请参阅[支持使用后台任务对应用程序](https://docs.microsoft.com/windows/uwp/launch-resume/support-your-app-with-background-tasks)。

有关使用 Windows 服务的信息，请参阅[Services](https://msdn.microsoft.com/library/windows/desktop/ms685141.aspx)。

## <a name="span-idconfirmkernelspanuse-the-driver-frameworks"></a><span id="confirmkernel"></span>使用驱动程序框架 

**安全核对清单项\#2:***使用驱动程序框架以减少代码的大小并提高其可靠性和安全性。*

使用[Windows 驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)以减少代码的大小并提高其可靠性和安全性。  若要开始，请查看[使用 WDF 开发驱动程序](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-to-develop-a-driver)。 有关使用较低风险用户模式 framework 驱动程序 (UMDF) 的信息，请参阅[选择驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/choosing-a-driver-model)。

编写一种旧方式[Windows 驱动程序模型 (WDM)](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)驱动程序是更耗时又耗费成本，并且几乎总是涉及重新创建位于驱动程序框架的代码。

Windows 驱动程序框架的源代码是开放源代码并在 GitHub 上可用。 这是从中生成在 Windows 10 中随附的 WDF 运行时库相同的源代码。 如果能够按照驱动程序和 WDF 之间的交互步骤进行操作，则可更有效地调试驱动程序。 从[ https://github.com/Microsoft/Windows-Driver-Frameworks ](https://github.com/Microsoft/Windows-Driver-Frameworks)。


## <a name="span-idcontrolsoftwareonlyspancontrol-access-to-software-only-drivers"></a><span id="controlsoftwareonly"></span>控制对软件仅驱动程序的访问

**安全核对清单项\#3:***如果要创建仅限软件的驱动程序，必须实现进一步的访问控制。*

仅限软件的内核驱动程序不使用和-插即用 (PnP) 若要将与特定硬件 Id，相关联，可以在任何 PC 上运行。 无法用于此类驱动程序，而不是最初计划，创建的攻击向量。 

仅限软件的内核驱动程序包含额外的风险，因为它们必须将限制 （例如，通过使用唯一的即插即用 ID 可创建的即插即用驱动程序，或通过检查存在特定的硬件的 SMBIOS 表） 在特定硬件上运行。

例如，假设的 OEM Fabrikam 想要分发的驱动程序，使其系统超频实用工具。  如果要从不同的 OEM 系统上执行此仅限软件的驱动程序，可能会导致系统不稳定或损坏。  Fabrikam 的系统应包括唯一的即插即用 ID 可创建的即插即用驱动程序，也是可通过 Windows Update 更新。  如果这不可能实现，并且 Fabrikam 名作者旧驱动程序，该驱动程序应找到另一种方法来验证，它在其上执行 Fabrikam 系统 （例如，通过启用任何功能之前的 SMBIOS 表的检查）。 


## <a name="span-iddonotproductionsignspan-do-not-production-sign-test-code"></a><span id="donotproductionsign"></span> 非生产标记测试代码

**安全核对清单项\#4:***执行不生产代码登录开发、 测试和生产内核驱动程序代码。*

用于开发的内核驱动程序代码，测试或生产可能包括危险会带来安全风险的功能。  此危险代码永远不会应使用 Windows 信任的证书进行签名。  正确的机制，用于执行危险的驱动程序代码是可以禁用 UEFI 安全引导、 BCD"TESTSIGNING"，并登录开发、 测试和生产代码中使用的不受信任的证书 （例如，makecert.exe 生成的一个）。

签名由受信任的软件发布者证书 (SPC) 或 Windows 硬件质量实验室 (WHQL) 签名的代码不利于提供跳过的 Windows 代码完整性和安全性技术。  代码签名由受信任的 SPC 或 WHQL 签名之前，先确保它满足中的指南[创建可靠的内核模式驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-reliable-kernel-mode-drivers)。 除了代码不得包含任何危险行为，如下所述。  有关驱动程序签名的详细信息，请参阅[版本驱动程序签名](#releasedriversigning)这篇文章中更高版本。

危险行为的示例包括：

- 提供相关功能来映射到用户模式下的任意内核、 物理、 或设备内存。
- 提供相关功能来读取或写入任意内核、 物理计算机或设备的内存，包括端口输入/输出 (I/O)。
- 提供访问绕过 Windows 访问控制的存储。 
- 提供相关功能来修改硬件或固件的驱动程序不被设计用于管理。  


## <a name="span-idthreatanalysisspanspan-idthreatanalysisspanspan-idthreatanalysisspanperform-threat-analysis"></a><span id="ThreatAnalysis"></span><span id="threatanalysis"></span><span id="THREATANALYSIS"></span>执行威胁分析


**安全核对清单项\#5:***请修改现有的驱动程序威胁模型或创建您的驱动程序的自定义的威胁模型。*

出于安全考虑，常见的方法是创建会描述的是可能的攻击类型的特定威胁模型。 设计一个驱动程序，因为它会强制开发人员需要预先考虑潜在的攻击媒介，针对一个驱动程序时，此方法很有用。 确定潜在威胁后，驱动程序开发人员则可以考虑防御这些威胁，从而有助于巩固理解驱动程序组件的总体安全性的方式。

本文提供了用于创建轻量的威胁模型的驱动程序特定指南：[威胁建模，驱动程序](threat-modeling-for-drivers.md)。 本文提供的示例驱动程序可以用作您的驱动程序的起始点的威胁模型关系图。

![假设的内核模式驱动程序的示例数据数据流关系图](images/sampledataflowdiagramkernelmodedriver.gif)

安全开发生命周期 (SDL) 最佳实践和相关的工具可通过 Ihv 和 Oem 以提高其产品的安全性。 有关详细信息请参阅[SDL 建议 oem](https://docs.microsoft.com/en-us/windows-hardware/drivers/bringup/security-overview#sdl-recommendations-for-oems)。


## <a name="span-iddriversecuritycodepracticesspanspan-iddriversecuritycodepracticesspanspan-iddriversecuritycodepracticesspanfollow-driver-secure-coding-guidelines"></a><span id="DriverSecurityCodePractices"></span><span id="driversecuritycodepractices"></span><span id="DRIVERSECURITYCODEPRACTICES"></span>遵循安全编码准则的驱动程序

**安全核对清单项\#6:***查看你的代码并删除任何已知的代码漏洞。*

创建安全的驱动程序的核心活动确定需要更改以避免已知的软件漏洞的代码中的区域。 许多这些已知的软件漏洞处理保留严格跟踪使用的内存以避免与其他人覆盖或否则组成您的驱动程序使用的内存位置的问题。

[代码验证工具](#codevalidationtools)这篇文章的部分介绍可用于帮助查找已知的软件漏洞的软件工具。


**内存缓冲区**

- 始终检查以确保缓冲区可以容纳所有请求的数据的输入和输出缓冲区的大小。 有关详细信息，请参阅[未能检查缓冲区大小](https://msdn.microsoft.com/library/windows/hardware/ff545679)。

- 正确地初始化用零之前将其返回给调用方的所有输出缓冲区。 有关详细信息，请参阅[无法初始化输出缓冲区](https://msdn.microsoft.com/library/windows/hardware/ff545693)。

- 验证长度可变的缓冲区。 有关详细信息，请参阅[验证长度可变的缓冲区失败](https://msdn.microsoft.com/library/windows/hardware/ff545709)。 有关使用缓冲区，并使用详细信息[ **ProbeForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559876)并[ **ProbeForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff559879)若要验证的地址缓冲区，请参阅[缓冲区处理](https://msdn.microsoft.com/library/windows/hardware/ff539004)。


**使用适当的方法来访问数据缓冲区与 Ioctl**

Windows 驱动程序的主要职责之一用户模式应用程序和系统的设备之间传输数据。 用于访问数据缓冲区的三种方法是下表中所示。 

|IOCTL 缓冲区类型 | 总结                                    | 更多相关信息 |  
|------------------|--------------------------------------------|-------------------------------------------------------------------------|
| METHOD_BUFFERED  |建议用于大多数通电无法            | [使用缓冲的 I/O](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-buffered-i-o)
| METHOD_IN_DIRECT 或 METHOD_OUT_DIRECT |在某些高速度 HW I/O 中使用    |[使用直接 I/O](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-direct-i-o) |
| METHOD_NEITHER |如果可能，避免 |[使用既不缓冲，也不直接 I/O](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-neither-buffered-nor-direct-i-o)|

一般情况下缓冲 I/O 建议，因为它提供了最安全的缓冲方法。 但即使使用缓冲的 I/O 有危险，如必须缓解的嵌入式指针。

有关使用 Ioctl 中的缓冲区的详细信息，请参阅[方法的访问数据缓冲区](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)。

**IOCTL 使用中的错误缓冲 I/O**

- 检查 IOCTL 大小相关的缓冲区。 有关详细信息，请参阅[未能检查缓冲区大小](https://msdn.microsoft.com/library/windows/hardware/ff545679)。
 
- 正确地初始化输出缓冲区。 有关详细信息，请参阅[无法初始化输出缓冲区](https://msdn.microsoft.com/library/windows/hardware/ff545693)。

- 正确验证长度可变的缓冲区。 有关详细信息，请参阅[验证长度可变的缓冲区失败](https://msdn.microsoft.com/library/windows/hardware/ff545709)。

- 当使用缓冲的 I/O，请确保并为 OutputBuffer 返回正确的长度[IO_STATUS_BLOCK](https://msdn.microsoft.com/library/windows/hardware/ff550671.aspx)结构信息字段。  只需直接不直接从读取请求返回的长度。  例如，假设用户空间中返回的数据指示没有 4 千字节缓冲区。  如果驱动程序实际上只应返回 200 个字节，而是在信息字段中只返回 4k 发生信息泄漏漏洞。 因为在早期版本的 Windows，I/O 管理器将用于缓冲 I/O 的缓冲区不归零，将发生此问题。  因此，用户应用重新获取原始 200 个字节的数据，以及 4k-200 个字节的任何内容时缓冲区 （非分页池内容） 中。 与所有缓冲 I/O 的使用和不只是 Ioctl，则会出现此情况。

**IOCTL 直接 I/O 中的错误**

正确处理的缓冲区长度为零。 有关详细信息，请参阅[直接 I/O 中的错误](https://msdn.microsoft.com/library/windows/hardware/ff544300)。

**引用用户空间地址中的错误**
- 验证指针嵌入在缓冲 I/O 请求。 有关详细信息，请参阅[中引用用户空间地址错误](https://msdn.microsoft.com/library/windows/hardware/ff544308)。

- 尝试使用它，如使用 Api 之前验证用户空间中的任一地址[ **ProbeForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559876)并[ **ProbeForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff559879)时适当。 

**TOCTOU 漏洞**

没有[潜在的使用时间的检查时](https://en.wikipedia.org/wiki/Time_of_check_to_time_of_use)(TOCTOU) 漏洞时使用直接 I/O （对于 Ioctl 或读/写）。  请注意，该驱动程序正在访问的用户数据缓冲区，它，同时可以访问用户。 

若要管理这种风险，请将复制需要对内存的只是验证从用户数据缓冲区的任何参数可访问从内核模式 （例如堆栈或池）。  然后后数据无法访问由用户应用程序，验证，然后传递中对数据进行操作。

**驱动程序代码必须进行正确的内存使用**

- 非可执行文件 (NX) 池中必须保持驱动程序的所有池分配。 使用 NX 内存池是本质上的安全性比使用可执行非分页 (NP) 池，并提供更好地保护以防止溢出攻击。 

- 设备驱动程序必须正确处理各种用户模式以及内核到内核 I/O 请求。 

若要允许驱动程序以支持 HVCI 虚拟化，有一些额外的内存要求。 有关详细信息，请参阅[设备防护兼容性](#dgc)这篇文章中更高版本。

**句柄**

- 验证用户模式和内核模式的内存之间传递的句柄。 有关详细信息，请参阅[处理管理](https://msdn.microsoft.com/library/windows/hardware/ff547382)并[验证对象将处理失败](https://msdn.microsoft.com/library/windows/hardware/ff545703)。

**设备对象**

- 保护设备对象。 有关详细信息，请参阅[保护设备对象](https://msdn.microsoft.com/library/windows/hardware/ff563688)。

- 验证设备的对象。 有关详细信息，请参阅[验证设备对象与失败](https://msdn.microsoft.com/library/windows/hardware/ff545700)。

**IRPs**

**WDF 和 Irp** 

使用 WDF 的一个优点是，WDF 驱动程序通常并不直接访问 Irp。 例如，框架将为表示框架 KMDF/UMDF I/O 队列中接收的请求对象的读取、 写入和设备 I/O 控制操作 WDM Irp。 

如果你正在编写 WDM 驱动程序，查看以下指南。

**正确地进行管理 IRP I/O 缓冲区**

以下文章提供有关验证 IRP 输入的值的信息：

[DispatchReadWrite 使用缓冲的 I/O](https://msdn.microsoft.com/library/windows/hardware/ff543388)

[中缓冲的 I/O 错误](https://msdn.microsoft.com/library/windows/hardware/ff544293)

[使用直接 I/O DispatchReadWrite](https://msdn.microsoft.com/library/windows/hardware/ff543393)

[在直接 I/O 错误](https://msdn.microsoft.com/library/windows/hardware/ff544300)

[I/O 控制代码的安全问题](https://msdn.microsoft.com/library/windows/hardware/ff563700)

请考虑验证与 IRP，如缓冲区地址和长度相关联的值。 

如果选择了使用既不 I/O，请注意，与不同的是读取和写入，并与不同的缓冲 I/O 和直接 I/O，，使用既不 I/O IOCTL 时缓冲区的指针和长度不是验证在 I/O 管理器。  


**正确处理 IRP 完成操作**

驱动程序必须永远不会完成状态将 status 值 IRP\_成功除非实际上支持，且处理 IRP。 有关处理 IRP 完成操作的正确方法的信息，请参阅[完成 Irp](https://msdn.microsoft.com/library/windows/hardware/ff542018)。

**管理驱动程序 IRP 挂起状态**

将保存 IRP，并且应考虑包含两个调用之前，该驱动程序应将标记挂起的 IRP [ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)和联锁序列中的分配。 有关详细信息，请参阅[未能检查驱动程序的状态](https://msdn.microsoft.com/library/windows/hardware/ff545672)并[保存传入 Irp 时设备暂停](https://docs.microsoft.com/windows-hardware/drivers/kernel/holding-incoming-irps-when-a-device-is-paused)。

**正确处理 IRP 取消操作**

取消操作可能会对代码很难正确因为它们通常以异步方式执行。 处理取消操作的代码中的问题可被忽略，长时间，因为执行此代码通常不经常在正在运行的系统中。 请务必阅读并理解所有下提供的信息[取消 Irp](https://msdn.microsoft.com/library/windows/hardware/ff540748)。 特别注意[同步 IRP 取消](https://msdn.microsoft.com/library/windows/hardware/ff564531)并[指向考虑时取消 Irp](https://msdn.microsoft.com/library/windows/hardware/ff559700)。

建议的方法之一，以最大程度减少与取消操作关联的同步问题是实现[取消安全 IRP 队列](https://msdn.microsoft.com/library/windows/hardware/ff540755)。

**处理 IRP 清理并正确关闭操作**

请务必了解之间的区别[ **IRP\_MJ\_清理**](https://msdn.microsoft.com/library/windows/hardware/ff550718)并[ **IRP\_MJ\_关闭** ](https://msdn.microsoft.com/library/windows/hardware/ff550720)请求。 清理请求到达后关闭的应用程序的所有句柄上的文件对象，但有时在所有 I/O 之前请求已完成。 关闭请求到达后的文件对象的所有 I/O 请求已完成或已取消。 有关详细信息，请参阅以下文章：

[DispatchCreate、 DispatchClose 和 DispatchCreateClose 例程](https://msdn.microsoft.com/library/windows/hardware/ff543279)

[DispatchCleanup 例程](https://msdn.microsoft.com/library/windows/hardware/ff543242)

[处理清除和关闭操作中的错误](https://msdn.microsoft.com/library/windows/hardware/ff544304)

了解如何正确处理 Irp 的详细信息，请参阅[还有其他错误处理 Irp](https://msdn.microsoft.com/library/windows/hardware/ff540543)。

**其他安全问题**

- 使用互锁的序列或锁来防止争用条件。 有关详细信息，请参阅[多处理器环境中的错误](https://msdn.microsoft.com/library/windows/hardware/ff544288)。

- 请确保设备驱动程序正确处理各种用户模式下以及内核到内核 I/O 请求。

- 确保任何 TDI 筛选器或 Lsp 安装驱动程序或关联的软件程序包在安装或使用情况。 

**使用安全函数**

- 使用安全的字符串函数。 有关详细信息，请参阅[使用安全字符串函数](https://msdn.microsoft.com/library/windows/hardware/ff565508)。

- 使用安全的算术函数。 有关详细信息，请参阅[算术函数](https://msdn.microsoft.com/library/windows/hardware/hh406348)中[安全整数库例程](https://msdn.microsoft.com/library/windows/hardware/hh406570)

- 使用安全的转换函数。 有关详细信息，请参阅[转换函数](https://msdn.microsoft.com/library/windows/hardware/hh450942)中[安全整数库例程](https://msdn.microsoft.com/library/windows/hardware/hh406570)

**其他代码漏洞**

除了本文所述的可能的漏洞，这篇文章提供了有关增强的内核模式驱动程序代码的安全性的其他信息：[创建可靠的内核模式驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff542904)。

有关 C 的其他信息和C++安全编码，请参阅[安全编码资源](#securecodingresources)本文末尾处。



## <a name="span-idmanagingdriveraccesscontrolspanspan-idmanagingdriveraccesscontrolspanspan-idmanagingdriveraccesscontrolspanmanage-driver-access-control"></a><span id="ManagingDriverAccessControl"></span><span id="managingdriveraccesscontrol"></span><span id="MANAGINGDRIVERACCESSCONTROL"></span>管理驱动程序的访问控制

**安全核对清单项\#7:***查看您的驱动程序以确保您正确地控制访问权限。*

**管理驱动程序的访问控制的 WDF**

驱动程序必须运行以防止用户不恰当地访问计算机的设备和文件。 若要防止未经授权的访问设备和文件，必须：

-   名称仅在必要时的设备对象。 指定的设备对象通常只是必要由于历史原因，例如如果你希望打开使用特定名称的设备的应用程序，或在使用非 PNP 设备/控制的设备。  请注意，WDF 驱动程序不需要命名它们即插即用设备 FDO 以便创建符号链接使用[WdfDeviceCreateSymbolicLink](https://msdn.microsoft.com/library/windows/hardware/ff545939.aspx)。

-   确保安全访问的设备对象和接口。 

若要允许应用程序或其他 WDF 驱动程序来访问你的即插即用设备 PDO，则应使用设备接口。 有关详细信息，请参阅[使用设备接口](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-device-interfaces)。 设备接口可作为设备堆栈的 PDO 的符号链接。 

控制对 PDO 的访问的 betters 方法之一是通过在你 INF 中指定的 SDDL 字符串。 如果的 SDDL 字符串不是 INF 文件中，Windows 将应用的默认安全描述符。 有关详细信息，请参阅[保护设备对象](https://docs.microsoft.com/windows-hardware/drivers/kernel/securing-device-objects)并[设备对象的 SDDL](https://docs.microsoft.com/windows-hardware/drivers/kernel/sddl-for-device-objects)。 

有关控制的访问权限的详细信息，请参阅以下文章：

[控制 KMDF 驱动程序中的设备访问权限](https://msdn.microsoft.com/windows/hardware/drivers/wdf/controlling-device-access-in-kmdf-drivers)

[名称、 安全描述符和设备类，使设备对象可访问...和安全](https://www.osr.com/nt-insider/2017-issue1/making-device-objects-accessible-safe)从*年 1 月 2017 年 2 月 NT 内幕新闻稿*由发布[OSR](https://www.osr.com)。


**管理驱动程序的访问控制-WDM**

如果你正在使用 WDM 驱动程序并使用指定的设备对象可以使用[IoCreateDeviceSecure](https://msdn.microsoft.com/library/windows/hardware/ff548407.aspx)并指定 SDDL 以进行保护。 当您实现[IoCreateDeviceSecure](https://msdn.microsoft.com/library/windows/hardware/ff548407.aspx)始终为 DeviceClassGuid 指定自定义类 GUID。 不应指定一个现有的类 GUID 此处。 这样做有可能会破坏安全设置或其他设备属于该类的兼容性。 有关详细信息，请参阅[WdmlibIoCreateDeviceSecure](https://msdn.microsoft.com/library/windows/hardware/mt800803.aspx)。
   
有关详细信息，请参阅以下文章：

[控制设备访问权限](https://msdn.microsoft.com/library/windows/hardware/ff542063)

[控制设备 Namespace 访问权限](https://msdn.microsoft.com/library/windows/hardware/ff542068)

[适用于驱动程序开发人员的 Windows 安全模型](windows-security-model.md)


**安全标识符 (Sid) 风险层次结构** 

以下部分介绍驱动程序代码中使用的常见 Sid 风险层次结构。 有关 SDDL 的常规信息，请参阅[设备对象的 SDDL](https://msdn.microsoft.com/library/windows/hardware/ff563667)， [SID 字符串](https://msdn.microsoft.com/library/windows/desktop/aa379602.aspx)，并[SDDL 字符串语法](https://msdn.microsoft.com/library/cc230374.aspx)。 

请务必了解较低特权调用方允许访问内核，请增加代码风险。 在此摘要图中，风险会增加对驱动程序功能允许较低权限的 Sid 的访问。

```cpp
SY (System)
\/
BA (Built-in Administrators)
\/
LS (Local Service)
\/
BU (Built-in User)
\/
AC (Application Container)
```

为遵循常规最少特权安全原则，配置只是所必需的驱动程序函数的访问权限的最低级别。

**WDM 精细 IOCTL 安全控制**

若要进一步管理安全 Ioctl 发送由用户模式下调用方时，驱动程序代码可以包括[IoValidateDeviceIoControlAccess](https://msdn.microsoft.com/library/windows/hardware/ff550418.aspx)函数。 此函数使驱动程序来检查访问权限。 一旦收到 IOCTL，驱动程序可以调用[IoValidateDeviceIoControlAccess](https://msdn.microsoft.com/library/windows/hardware/ff550418.aspx)，指定 FILE_READ_ACCESS、 FILE_WRITE_ACCESS，或这两者。 

实现精细 IOCTL 安全控件不会替换需要管理驱动程序访问使用上文所述的技术。

有关详细信息，请参阅以下文章：

[定义 I/O 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)


## <a name="span-iddgcspanspan-iddgcspanvalidate-device-guard-compatibility"></a><span id="DGC"></span><span id="dgc"></span>验证 Device Guard 兼容性

**安全核对清单项\#8:***验证您的驱动程序使用内存，以便它 Device Guard 兼容。*

**内存使用情况和 Device Guard 兼容性**

设备防护使用硬件技术和虚拟化来隔离系统的其余部分中的代码完整性 (CI) 决策制定函数。 当使用基于虚拟化的安全隔离 CI，内核内存可能会变得可执行文件的唯一方法是通过 CI 验证。 这意味着可写内容和可执行文件 (W + X) 的内核内存页面可以永远不会是不能直接修改可执行代码。 

若要实现 Device Guard 兼容代码，请确保您的驱动程序代码将执行以下操作：

- 选择启用 NX 默认情况下
- 有关内存分配 (NonPagedPoolNx) 使用 NX Api/标志
- 不使用是可写和可执行文件的部分
- 不会尝试直接修改可执行文件系统内存
- 不在内核中使用动态代码
- 不会加载为可执行文件的数据文件
- 节对齐是倍数 0x1000 (页\_大小)。 例如 驱动程序\_对齐方式 = 0x1000

有关使用该工具并不兼容的内存的调用列表的详细信息，请参阅[使用设备防护准备工具来评估 HVCI 驱动程序兼容性](use-device-guard-readiness-tool.md)。

了解 Device Guard 的常规信息，请参阅[驱动程序兼容性 Windows 10 中的 Device Guard](https://blogs.msdn.microsoft.com/windows_hardware_certification/2015/05/22/driver-compatibility-with-device-guard-in-windows-10/)。

有关相关的系统基础知识安全测试的详细信息，请参阅[Device Guard 的法规遵从性测试](https://docs.microsoft.com/en-us/windows-hardware/test/hlk/testref/10c242b6-49f6-491d-876c-c39b22b36abc)并[驱动程序兼容性 Device Guard](https://docs.microsoft.com/en-us/windows-hardware/test/hlk/testref/driver-compatibility-with-device-guard)。



## <a name="span-idtechnologyspecificcodepracticesspanfollow-technology-specific-code-best-practices"></a><span id="technologyspecificcodepractices"></span>遵循特定于技术的代码的最佳做法


**安全核对清单项\#9:***查看您的驱动程序的以下特定于技术的指南。*

*文件系统*

有关详细信息，有关文件系统驱动程序的安全性请参阅以下文章：

[文件系统的安全注意事项](https://msdn.microsoft.com/windows/hardware/drivers/ifs/security-considerations-for-file-systems)

[文件系统安全问题](https://msdn.microsoft.com/windows/hardware/drivers/ifs/file-system-security-issues)

[对于文件系统的安全功能](https://msdn.microsoft.com/windows/hardware/drivers/ifs/security-features-for-file-systems)

[文件系统筛选器驱动程序的安全注意事项](https://msdn.microsoft.com/windows/hardware/drivers/ifs/security-considerations-for-file-system-filter-drivers)

*NDIS-网络*

有关 NDIS 驱动程序的安全性的信息，请参阅[网络驱动程序的安全问题](https://msdn.microsoft.com/windows/hardware/drivers/network/security-issues-for-network-drivers)。

*显示器*

有关显示驱动程序的安全性的信息，请参阅&lt;内容挂起&gt;。


*打印机*

与打印机驱动程序的安全性相关的信息，请参阅[V4 打印机驱动程序的安全注意事项](https://msdn.microsoft.com/library/windows/hardware/jj863679)。

*Windows 图像采集 (WIA) 驱动程序的安全问题*

有关 WIA 安全性的信息，请参阅[安全问题的 Windows 图像采集 (WIA) 驱动程序](https://msdn.microsoft.com/windows/hardware/drivers/image/security-issues-for-wia-drivers)。



## <a name="span-idenhancedeviceinstallationsecurityspanenhance-device-installation-security"></a><span id="enhancedeviceinstallationsecurity"></span>增强设备安装的安全性

**安全核对清单项\#10:***查看驱动程序 inf 创建和安装指南以确保您按照最佳做法。*

创建安装您的驱动程序的代码时，必须确保以安全的方式将始终执行你的设备的安装。 安全设备安装是指执行以下任务：
 
- 限制对设备和其设备接口类的访问
- 设备创建的驱动程序服务的限制访问
- 驱动程序文件可防止修改或删除操作
- 限制对设备的注册表项的访问
- 限制对设备的 WMI 类的访问
- 正确使用安装程序 Api 函数

有关详细信息，请参阅以下文章：

[创建安全的设备安装](https://msdn.microsoft.com/windows/hardware/drivers/install/creating-secure-device-installations)

[使用 SetupAPI 的准则](https://msdn.microsoft.com/windows/hardware/drivers/install/guidelines-for-using-setupapi)

[使用设备安装函数](https://msdn.microsoft.com/windows/hardware/drivers/install/using-device-installation-functions)

[设备和驱动程序安装高级主题](https://msdn.microsoft.com/windows/hardware/drivers/install/device-and-driver-installation-advanced-topics)



## <a name="span-idpeercodereviewspanperform-peer-code-review"></a><span id="peercodereview"></span>执行对等代码评审

**安全核对清单项\#11:***执行对等代码评审，以查找未显示的其他工具和过程的问题*

找出知识渊博的专家代码审阅者来查找你可能错失的问题。 第二个集的眼睛通常会看到您可能已经忽略的问题。

如果没有合适的人员能够在内部检查您的代码，则考虑使用外部帮助实现此目的。



## <a name="span-idreleasedriversigningspanspan-idreleasedriversigningspanspan-idreleasedriversigningspanexecute-proper-release-driver-signing"></a><span id="ReleaseDriverSigning"></span><span id="releasedriversigning"></span><span id="RELEASEDRIVERSIGNING"></span>执行适当版本的驱动程序签名


**安全核对清单项\#12:***使用 Windows 合作伙伴门户进行正确签名驱动程序进行分发。*

在公开发布驱动程序包之前，我们建议你先提交程序包以进行认证。 有关详细信息，请参阅[测试的性能和兼容性](https://msdn.microsoft.com/windows/hardware/commercialize/test/index)，[开始使用硬件计划](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/get-started-with-the-hardware-dashboard)，[硬件仪表板服务](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/dashboard-services)，和[公开发行版的内核驱动程序签名的证明](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/attestation-signing-a-kernel-driver-for-public-release)。



## <a name="span-iduse-code-analysisspanuse-code-analysis-in-visual-studio-to-investigate-driver-security"></a><span id="use-code-analysis"></span>使用 Visual Studio 中的代码分析来调查驱动程序的安全性

**安全核对清单项\#13:***请按照这些步骤使用 Visual Studio 中的代码分析功能来检查驱动程序代码中的漏洞。*

使用 Visual Studio 中的代码分析功能来检查你的代码中的安全漏洞。 Windows Driver Kit (WDK) 安装的规则集，可用于检查本机驱动程序代码中的问题。

有关详细信息，请参阅[如何运行代码分析的驱动程序](https://msdn.microsoft.com/windows/hardware/drivers/devtest/how-to-run-code-analysis-for-drivers)。

有关详细信息，请参阅[的代码分析驱动程序概述](https://msdn.microsoft.com/library/windows/hardware/hh698231.aspx)。 代码分析的其他背景信息，请参阅[Visual Studio 2013 中的静态代码分析深度](https://blogs.msdn.microsoft.com/hkamel/2013/10/24/visual-studio-2013-static-code-analysis-in-depth-what-when-and-how/)。

若要熟悉代码分析，可以使用示例中，功能完备的 toaster 示例中，示例驱动程序之一<https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster/toastDrv/kmdf/func/featured>ELAM 早期启动反恶意软件示例或<https://github.com/Microsoft/Windows-driver-samples/tree/master/security/elam>。

1. 在 Visual Studio 中打开驱动程序解决方案。

2. 在 Visual Studio 中，为解决方案中每个项目更改项目属性，以使用所需的规则集。 例如：项目&gt;&gt;属性&gt;&gt;代码分析&gt;&gt;常规，选择*建议驱动程序规则*。 除了使用 recommenced 驱动程序规则，使用*建议本机规则*规则集。

3. 选择生成&gt;&gt;对解决方案运行代码分析。

4. 查看中的警告**错误列表**选项卡上的生成输出窗口 Visual Studio 中的。

单击每个警告，若要查看存在问题的地方在代码中的说明。

单击链接的警告代码，以了解其他信息。

确定是否需要更改，你的代码或批注是否需要添加要允许代码分析引擎，以正确地遵循代码的意图。 代码注释的详细信息，请参阅[使用 SAL 注释减少 C /C++代码缺陷](https://msdn.microsoft.com/library/ms182032.aspx)并[SAL 2.0 注释为 Windows 驱动程序](https://msdn.microsoft.com/windows/hardware/drivers/devtest/sal-2-annotations-for-windows-drivers)。

SAL 的常规信息，请参阅此文章提供从 OSR。
https://www.osr.com/blog/2015/02/23/sal-annotations-dont-hate-im-beautiful/

## <a name="span-idsdvspanspan-idsdvspanuse-static-driver-verifier-to-check-for-vulnerabilities"></a><span id="SDV"></span><span id="sdv"></span>使用 Static Driver Verifier 漏洞检查

**安全核对清单项\#14:***请按照下列步骤以在 Visual Studio 中使用 Static Driver Verifier (SDV) 检查驱动程序代码中的漏洞。*

Static Driver Verifier (SDV) 使用一组接口规则和操作系统的模型来确定是否与 Windows 操作系统驱动程序交互正确。 SDV 可以指向驱动程序中的潜在错误的驱动程序代码中查找缺陷。

有关详细信息，请参阅[简介 Static Driver Verifier](https://msdn.microsoft.com/windows/hardware/drivers/devtest/introducing-static-driver-verifier)并[Static Driver Verifier](https://msdn.microsoft.com/windows/hardware/drivers/devtest/static-driver-verifier)。 请注意，SDV 支持某些类型的驱动程序。 SDV 可以验证驱动程序有关的详细信息，请参阅[支持的驱动程序](https://msdn.microsoft.com/windows/hardware/drivers/devtest/supported-drivers)。

若要熟悉 SDV，可以使用其中一个示例驱动程序 (例如，功能完备的 toaster 示例： <https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster/toastDrv/kmdf/func/featured>)。

1. 在 Visual Studio 中打开目标驱动程序解决方案。

2. 在 Visual Studio 中，将生成类型更改为*版本*。 Static Driver Verifier 要求生成类型版本中，不调试。

3. 在 Visual Studio 中，选择生成&gt;&gt;生成解决方案。

4. 在 Visual Studio 中，选择驱动程序&gt;&gt;启动 Static Driver Verifier。

5. SDV，在上*规则*选项卡上，选择*默认*下*规则集*。

尽管默认规则将发现许多常见的问题，请考虑运行更广泛*驱动程序的所有规则*规则集以及。

6. 上*Main*选项卡的 SDV，单击*启动*。

7. SDV 完成后，查看输出中的任何警告。 *Main*选项卡显示发现的缺陷的总数。

8. 单击每个警告，以加载 SDV 报表页，并检查与可能的代码漏洞有关的信息。 使用报表来调查验证结果并标识失败 SDV 验证驱动程序中的路径。 有关详细信息，请参阅[静态驱动程序验证工具报告](https://msdn.microsoft.com/library/windows/hardware/ff552834)。




## <a name="span-idbinscopespanspan-idbinscopespanspan-idbinscopespancheck-code-with-binscope-binary-analyzer"></a><span id="BinScope"></span><span id="binscope"></span><span id="BINSCOPE"></span>通过 BinScope 二进制分析器检查代码

**安全核对清单项\#15:***请按照这些步骤使用 BinScope 仔细检查的编译和生成选项配置为最小化的已知的安全问题。*

使用 BinScope 检查应用程序二进制文件，以确定编写和构建可能可以呈现应用程序容易受到攻击或被用作攻击媒介，易受攻击的做法。

有关详细信息，请参阅[新版本的 BinScope 二进制分析器](https://cloudblogs.microsoft.com/microsoftsecure/2014/11/20/new-binscope-released/)，用户和入门指南，它们包含在下载的工具。


请按照下列步骤来验证安全编译选项都正确配置为传送的代码中：

1. 从此处下载 BinScope 分析器和相关的文档： <https://www.microsoft.com/download/details.aspx?id=44995>。

2. 审阅*BinScope 入门指南*下载。

3. 使用 MSI 文件包含你想要验证的已编译的代码的目标测试计算机上安装 BinScope。

4. 打开命令提示符窗口并执行以下命令以检查已编译的驱动程序二进制文件。 更新以指向你的已编译的驱动程序.sys 文件的路径。

```cpp
C:\Program Files\Microsoft BinScope 2014>binscope "C:\Samples\KMDF_Echo_Driver\echo.sys" /verbose /html /logfile c:\mylog.htm 
```

5. 使用浏览器查看 BinScope 报告以确认所有检查都标记 (PASS)。

默认情况下，HTML 报表写入到\\用户\\&lt;用户名&gt;\\BinScope\\

有可能是输出到日志文件的三个类别：

-   失败的检查\[失败\]
-   未完成的检查\[错误\]
-   通过检查\[传递\]

请注意，通过的检查未写入到日志默认情况下，必须使用启用 /verbose 切换。

```cpp
Results for Microsoft BinScope 2014 run on MyPC at 2017-01-28T00:18:48.3828242Z

Failed Checks
No failed checks. 
Passed Checks

• C:\Samples\KMDF_Echo_Driver\echo.sys - ATLVersionCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - ATLVulnCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - CompilerVersionCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - DBCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - DefaultGSCookieCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - ExecutableImportsCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - GSCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - GSFriendlyInitCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - GSFunctionSafeBuffersCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - HighEntropyVACheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - NXCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - RSA32Check (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - SafeSEHCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - SharedSectionCheck (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - VB6Check (PASS)
• C:\Samples\KMDF_Echo_Driver\echo.sys - WXCheck (PASS)

Checks Executed:
• ATLVersionCheck
• ATLVulnCheck
• CompilerVersionCheck
• DBCheck
• DefaultGSCookieCheck
• ExecutableImportsCheck
• GSCheck
• GSFriendlyInitCheck
• GSFunctionSafeBuffersCheck
• HighEntropyVACheck
• NXCheck
• RSA32Check
• SafeSEHCheck
• SharedSectionCheck
• VB6Check
• WXCheck

All Scanned Items

• C:\Samples\KMDF_Echo_Driver\echo.sys
```

## <a name="span-idcodevalidationtoolsspanspan-idcodevalidationtoolsspanspan-idcodevalidationtoolsspanuse-additional-code-validation-tools"></a><span id="CodeValidationTools"></span><span id="codevalidationtools"></span><span id="CODEVALIDATIONTOOLS"></span>使用其他代码验证工具

**安全核对清单项\#16:***若要帮助验证你的代码，如下所示的安全建议和探测的开发过程中缺少的间隙，请使用这些额外的工具。*

除了[Visual Studio Code analysis](#use-code-analysis)， [Static Driver Verifier](#sdv)，并[Binscope](#binscope)上文所述，使用以下工具来探测间隔中有丢失的应用开发过程。

**驱动程序验证程序**

驱动程序验证程序便可以实时测试的驱动程序。 驱动程序验证工具可监视 Windows 内核模式驱动程序和图形驱动程序以检测非法的函数调用或可能会损坏系统的操作。 驱动程序验证程序可以使用者到各种压力和测试，以找到不正确的行为的 Windows 驱动程序。 有关详细信息，请参阅[Driver Verifier](https://msdn.microsoft.com/windows/hardware/drivers/devtest/driver-verifier)。

**硬件兼容性计划测试**

硬件兼容性计划包括安全相关的测试可用于查找代码漏洞。 Windows 硬件兼容性计划利用 Windows 硬件 Lab Kit (HLK) 中的测试。 HLK 设备基础测试可以在命令行上，用于驱动程序代码和漏洞的探测。 有关设备基础测试和硬件兼容性计划的常规信息，请参阅[Windows 硬件实验室工具包](https://docs.microsoft.com/en-us/windows-hardware/test/hlk/windows-hardware-lab-kit)。

以下测试是可能会在可用于检查与代码漏洞关联一些行为的驱动程序代码的测试的示例：

 [DF - 模糊随机 IOCTL 测试（可靠性）](https://docs.microsoft.com/windows-hardware/test/hlk/testref/236b8ad5-0ba1-4075-80a6-ae9dafb71c94)

 [DF - 模糊 sub-open 测试（可靠性）](https://docs.microsoft.com/windows-hardware/test/hlk/testref/92bf534e-aa48-4aeb-b3cd-e46fb7cc7d80)

 [DF - 模糊零长度缓冲区 FSCTL 测试（可靠性）](https://docs.microsoft.com/windows-hardware/test/hlk/testref/5f5f6c7e-d5db-4ff1-8cee-da47203ab070)

 [DF - 模糊随机 FSCTL 测试（可靠性）](https://docs.microsoft.com/windows-hardware/test/hlk/testref/e529e34e-076a-4978-926f-7eca333e8f4d)

 [DF - 模糊杂项 API 测试（可靠性）](https://docs.microsoft.com/windows-hardware/test/hlk/testref/fb305d04-6e8c-4dfc-9984-9692df82fbd8)

 此外可以使用[内核同步延迟模糊](https://docs.microsoft.com/windows-hardware/drivers/devtest/kernel-synchronization-delay-fuzzing)随驱动程序验证程序。

（并发硬件和操作系统） 的混沌测试运行各种即插即用驱动程序测试、 设备驱动程序模糊测试，并关闭系统同时测试。 有关详细信息，请参阅[混沌测试 （设备基础）](https://docs.microsoft.com/en-us/windows-hardware/drivers/devtest/chaos-tests--device-fundamentals-)。

设备的基础知识渗透测试执行各种形式的输入攻击，安全测试的重要组成部分。 攻击和渗透测试可帮助确定在软件界面中的漏洞。 有关详细信息，请参阅[渗透测试 （设备基础）](https://docs.microsoft.com/en-us/windows-hardware/drivers/devtest/penetration-tests--device-fundamentals-)。

使用[Device Guard 的法规遵从性测试](https://docs.microsoft.com/en-us/windows-hardware/test/hlk/testref/10c242b6-49f6-491d-876c-c39b22b36abc)，以及在本文中，若要确认您的驱动程序是否兼容的 Device Guard 中所述的其他工具。


**自定义和特定于域的测试工具**

请考虑开发自定义特定于域的安全测试。 若要开发其他测试，收集的软件，以及熟悉正在开发的驱动程序的特定类型的不相关的开发资源的原始设计器和一个或多个人员熟悉安全入侵分析从输入和防护。



## <a name="span-iddebuggerspanspan-iddebuggerspanspan-iddebuggerspanreview-debugger-techniques-and-extensions"></a><span id="Debugger"></span><span id="debugger"></span><span id="DEBUGGER"></span>查看调试器技术和扩展


**安全核对清单项\#17:***查看这些集成调试器的工具，考虑在调试工作流开发中的使用它们。*

**！ 可利用 Crash Analyzer**

！ 可利用故障分析器是分析崩溃日志查找特有的问题的 Windows 调试器扩展。 它还检查崩溃的类型，并尝试确定错误是否是内容可能被恶意黑客利用。

Microsoft Security Engineering Center (MSEC)，创建 ！ 可利用 Crash Analyzer。 您可以下载从 codeplex: <https://msecdbg.codeplex.com/>。

有关详细信息，请参阅[！可利用故障分析器版本 1.6](https://blogs.microsoft.com/microsoftsecure/2013/06/13/exploitable-crash-analyzer-version-1-6/)和第 9 频道视频[！ 可利用故障分析器](https://channel9.msdn.com/blogs/pdcnews/bang-exploitable-security-analyzer)。

**与安全相关的调试器命令**

！ Acl 扩展设置格式并显示内容的访问控制列表 (ACL)。 有关详细信息，请参阅[确定对象的 ACL](https://msdn.microsoft.com/library/windows/hardware/ff541868)并[ **！ acl**](https://msdn.microsoft.com/library/windows/hardware/ff561510)。

！ 令牌的扩展插件都会显示一个安全令牌对象的格式化的视图。 有关详细信息，请参阅[ **！ 令牌**](https://msdn.microsoft.com/library/windows/hardware/ff565477)。

！ Tokenfields 扩展显示名称和访问令牌对象 （标记结构） 中的字段的偏移量。 有关详细信息，请参阅[ **！ tokenfields**](https://msdn.microsoft.com/library/windows/hardware/ff565478)。

！ Sid 扩展显示指定地址处的安全标识符 (SID)。 有关详细信息，请参阅[ **！ sid**](https://msdn.microsoft.com/library/windows/hardware/ff565344)。

！ Sd 扩展显示指定地址处的安全描述符。 有关详细信息，请参阅[ **！ sd**](https://msdn.microsoft.com/library/windows/hardware/ff564930)。


## <a name="span-idsecurecodingresourcesspanspan-idsecurecodingresourcesspanspan-idsecurecodingresourcesspanreview-secure-coding-resources"></a><span id="SecureCodingResources"></span><span id="securecodingresources"></span><span id="SECURECODINGRESOURCES"></span>查看安全编码资源


**安全核对清单项\#18:***查看这些资源，以展开您对适用于驱动程序开发人员的安全编码最佳实践的理解。*

*查看这些资源，若要了解有关驱动程序的安全性的详细信息*

**安全内核模式驱动程序编码指南**

[创建可靠的内核模式驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff542904.aspx)

**安全编码组织**

[卡耐基-梅隆大学 SEI 证书](https://www.cert.org/)

卡耐基-梅隆大学 SEI CERT[编码标准的 C:用于开发安全、 可靠且安全的系统规则](https://www.securecoding.cert.org/confluence/display/c/SEI+CERT+C+Coding+Standard)（2016年版）。

证书-[构建安全性](https://www.us-cert.gov/bsi)

MITRE-[漏洞所处理的 CERT C 安全编码标准](https://cwe.mitre.org/data/definitions/734.html)

构建安全的成熟度模型 (BSIMM)- [https://www.bsimm.com/](https://www.bsimm.com/)

SAFECode - [https://www.safecode.org/](https://www.safecode.org/)


**OSR**

[OSR](https://www.osr.com)提供培训和咨询服务的驱动程序开发。 以下文章从 OSR 时事通讯重点介绍驱动程序的安全问题。

[名称、 安全描述符和设备类，使设备对象可访问...和安全](https://www.osr.com/nt-insider/2017-issue1/making-device-objects-accessible-safe)

[您已经走使用保护--在驱动程序和设备安全性](https://www.osronline.com/article.cfm?article=100)

[锁定驱动程序的技术的调查](https://www.osronline.com/article.cfm?article=357) 

[Meltdown 和 Spectre:驱动程序呢？](https://www.osr.com/blog/2018/01/23/meltdown-spectre-drivers/) 

**案例研究**

[从驱动程序漏洞的警报：Microsoft Defender ATP 调查 unearths 权限提升漏洞](https://www.microsoft.com/security/blog/2019/03/25/from-alert-to-driver-vulnerability-microsoft-defender-atp-investigation-unearths-privilege-escalation-flaw/)


**丛书**

*软件安全性的 24 deadly sins： 编程缺陷以及如何解决这些问题*由 Michael Howard、 David LeBlanc 和 John Viega

*软件安全评估的艺术： 识别和防止出现软件漏洞*，Mark Dowd、 John McDonald 和 Justin Schuh

*编写安全的软件的第二版*，Michael Howard 和 David LeBlanc

*软件安全评估的技术：识别和防止出现软件漏洞*，Mark Dowd 和 John McDonald

*安全编码在 C 和C++（SEI 系列在软件工程） 版本 2*，C.为 Robert Seacord

*Microsoft Windows 驱动程序的编程模型 （第二版）*，Walter Oney

*开发驱动程序使用 Windows Driver Foundation （开发人员参考）*，Penny Orwick 和 Smith 专家 


**培训**

Windows 驱动程序课堂培训是可从供应商，如下所示：

- [OSR](https://www.osr.com) 
- [Winsider](https://www.windows-internals.com/)
- [Azius](https://www.azius.com)

安全编码在线培训提供了不同的源。 例如，本课程是从 coursera 可用：

[https://www.coursera.org/learn/software-security](https://www.coursera.org/learn/software-security).

SAFECode 提供免费培训以及：

[SAFECode.org/training](https://safecode.org/training/)

**专业人员认证**

 CERT 提供[安全编码专业认证](https://www.cert.org/go/secure-coding/)。


## <a name="span-idkeytakeawaysspansummary-of-key-takeaways"></a><span id="keytakeaways"></span>关键结论的摘要

驱动程序的安全性是复杂的工作，其中包含许多元素，但以下是要考虑的几个要点：

-   驱动程序位于 windows 内核中，并在内核中执行时遇到问题公开整个操作系统。 因此，请特别注意到驱动程序的安全性和设计考虑到了安全性。

-   应用最小特权原则：

    a.  使用严格的 SDDL 字符串来限制对该驱动程序的访问

    b.  进一步限制单个 IOCTL 

-   创建威胁模型来确定的攻击媒介，并考虑是否任何内容可限制更多。
-   请注意关于嵌入式指针传入从用户模式。 它们需要探测，内部除外，请尝试进行访问，除非捕获并比较的缓冲区的值，它们是易于检查的使用 (ToCToU) 问题的时间的时间。
-   如果您不确定，则使用 METHOD_BUFFERED 作为 IOCTL 缓冲方法。
-   使用代码扫描实用程序来查找已知的代码漏洞和修正发现的任何问题。
-   找出知识渊博的专家代码审阅者来查找你可能错失的问题。
-   使用驱动程序验证程序和测试您的驱动程序具有多个输入，包括极端状况。

 

[向 Microsoft 发送有关本文的注释](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[hw_design/hw_design]:%20Driver%20security%20checklist%20%20RELEASE:%20%286/16/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20 https://privacy.microsoft.com/default.aspx. "向 Microsoft 发送有关本主题的注释")





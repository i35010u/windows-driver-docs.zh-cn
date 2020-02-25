---
title: 驱动程序安全清单
description: 本文为驱动程序开发人员提供了驱动程序安全核对清单。
ms.assetid: 25375E02-FCA1-4E94-8D9A-AA396C909278
ms.date: 04/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: d2336302cae77e9a4690f0afd20e1b77ac7e0212
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528977"
---
# <a name="driver-security-checklist"></a>驱动程序安全清单

本文为驱动程序开发人员提供了驱动程序安全清单，以帮助降低驱动程序被泄露的风险。

## <a name="span-iddriver_security_overviewspanspan-iddriver_security_overviewspanspan-iddriver_security_overviewspandriver-security-overview"></a><span id="Driver_Security_Overview"></span><span id="driver_security_overview"></span><span id="DRIVER_SECURITY_OVERVIEW"></span>驱动程序安全性概述

安全漏洞是指允许攻击者导致驱动程序故障的任何缺陷，使系统崩溃或变得不可用。 此外，驱动程序代码中的漏洞可能允许攻击者获取对内核的访问权限，从而可能危及整个操作系统的安全。 当大多数开发人员处理其驱动程序时，其重点是使驱动程序正常工作，而不是恶意攻击者是否会尝试利用其代码中的漏洞。

但是，在释放驱动程序后，攻击者可能会尝试探测并识别安全漏洞。 开发人员必须在设计和实施阶段考虑这些问题，以最大程度地减少此类漏洞的可能性。 目标是在驱动程序发布之前消除所有已知的安全漏洞。

创建更安全的驱动程序需要系统架构师（特意考虑驱动程序潜在威胁）、实现代码的开发人员（保守编码可能成为攻击来源的常见操作）以及测试团队（主动尝试查找弱点和漏洞）。 通过适当地协调所有这些活动，驱动程序的安全性大大增强。

除了避免与受攻击的驱动程序相关的问题，所述的许多步骤（如更精确地使用内核内存）也会提高驱动程序的可靠性。 这将降低支持成本，并提高客户对产品的满意度。 完成以下清单中的任务可帮助实现所有这些目标。

**安全清单：** *完成其中每个主题中所述的安全任务。*

![空复选框](images/checkbox.png)[确认需要内核驱动程序](#confirmkernel)

![空复选框](images/checkbox.png)[使用驱动程序框架](#confirmkernel)

![空复选框](images/checkbox.png)[控制对仅软件驱动程序的访问](#controlsoftwareonly)

![空复选框，](images/checkbox.png)[则不会为生产签署测试驱动程序代码](#donotproductionsign)

![空复选框](images/checkbox.png)[执行威胁分析](#threatanalysis)

![空复选框](images/checkbox.png)[遵循驱动程序安全编码准则](#driversecuritycodepractices)

![空复选框](images/checkbox.png)[验证设备保护兼容性](#dgc)

![空复选框](images/checkbox.png)[遵循特定于技术的代码最佳做法](#technologyspecificcodepractices)

![空复选框](images/checkbox.png)[执行对等代码评审](#peercodereview)

"![空" 复选框](images/checkbox.png)[管理驱动程序访问控制](#managingdriveraccesscontrol)

![空复选框](images/checkbox.png)[增强设备安装安全性](#enhancedeviceinstallationsecurity)

![空复选框则](images/checkbox.png)[执行正确的版本驱动程序签名](#releasedriversigning)

![空复选框](images/checkbox.png)[在 Visual Studio 中使用代码分析来调查驱动程序安全性](#use-code-analysis)

![空复选框](images/checkbox.png)[使用静态驱动程序验证程序检查是否存在漏洞](#sdv)

![空复选框](images/checkbox.png)[检查带有 Binscope 二进制分析器的代码](#binscope)

![空复选框](images/checkbox.png)[使用代码验证工具](#codevalidationtools)

![空复选框](images/checkbox.png)[查看调试器技术和扩展](#debugger)

![空复选框](images/checkbox.png)[查看安全编码资源](#securecodingresources)

[要点总结](#keytakeaways)

## <a name="span-idconfirmkernelspanconfirm-that-a-kernel-driver-is-required"></a><span id="confirmkernel"></span>确认需要内核驱动程序

**安全核对清单项 \#1：** *确认需要内核驱动程序，并且不能更好地选择较低的风险方法（如 Windows 服务或应用）。*

Windows 内核中的驱动程序在内核中执行时会出现问题。 如果有任何其他选项可用，则与创建新的内核驱动程序相比，它可能会降低成本并降低关联的风险。
有关使用内置 Windows 驱动程序的详细信息，请参阅[是否需要编写驱动程序？](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/do-you-need-to-write-a-driver-)。

有关使用后台任务的信息，请参阅使用[后台任务支持应用](https://docs.microsoft.com/windows/uwp/launch-resume/support-your-app-with-background-tasks)。

有关使用 Windows 服务的信息，请参阅[服务](https://docs.microsoft.com/windows/desktop/Services/services)。

## <a name="span-idconfirmkernelspanuse-the-driver-frameworks"></a><span id="confirmkernel"></span>使用驱动程序框架

**安全清单项 \#2：** *使用驱动程序框架减小代码大小并提高其可靠性和安全性。*

使用[Windows 驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)减小代码大小并提高其可靠性和安全性。  若要开始，请查看[使用 WDF 开发驱动程序](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-to-develop-a-driver)。 有关使用低风险用户模式框架驱动程序（UMDF）的信息，请参阅[选择驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/choosing-a-driver-model)。

编写旧的方式[Windows 驱动模型（WDM）](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)驱动程序需要花费更多时间，并且几乎始终都需要重新创建驱动程序框架中提供的代码。

Windows 驱动程序框架源代码是开放源代码，在 GitHub 上可用。 这与 Windows 10 中随附的 WDF 运行时库生成的源代码相同。 如果能够按照驱动程序和 WDF 之间的交互步骤进行操作，则可更有效地调试驱动程序。 从[https://github.com/Microsoft/Windows-Driver-Frameworks](https://github.com/Microsoft/Windows-Driver-Frameworks)下载。

## <a name="span-idcontrolsoftwareonlyspancontrol-access-to-software-only-drivers"></a><span id="controlsoftwareonly"></span>控制对仅软件驱动程序的访问

**安全清单项 \#3：** *如果要创建仅软件驱动程序，则必须实现其他访问控制。*

仅软件内核驱动程序不使用即插即用（PnP）与特定硬件 Id 相关联，并且可以在任何电脑上运行。 此类驱动程序可用于除最初目的之外的其他用途，从而创建攻击向量。

由于仅软件内核驱动程序包含额外的风险，因此必须将其限制为在特定硬件上运行（例如，通过使用唯一的 PnP ID 启用 PnP 驱动程序的创建，或检查 SMBIOS 表中是否存在特定硬件）。

例如，假设 OEM Fabrikam 要分发一个驱动程序，该驱动程序为其系统启用超频实用程序。  如果要在不同 OEM 的系统上执行此仅软件驱动程序，则可能会导致系统不稳定或损坏。  Fabrikam 的系统应包含唯一的 PnP ID，以允许创建也可通过 Windows 更新更新的 PnP 驱动程序。  如果这是不可能的，并且 Fabrikam 作者是旧的驱动程序，则该驱动程序应找到另一种方法来验证它是否正在 Fabrikam 系统上执行（例如，在启用任何功能之前通过检查 SMBIOS 表）。

## <a name="span-iddonotproductionsignspan-do-not-production-sign-test-code"></a><span id="donotproductionsign"></span>不生产签名测试代码

**安全清单项 \#4：** *不生成代码签名开发、测试和制造内核驱动程序代码。*

用于开发、测试或制造的内核驱动程序代码可能包含带来安全风险的危险功能。  此危险代码决不会使用 Windows 信任的证书进行签名。  执行危险驱动程序代码的正确机制是禁用 UEFI 安全启动，启用 BCD "TESTSIGNING"，并使用不受信任的证书（例如，由 makecert 生成的证书）对开发、测试和制造代码进行签名。

受信任的软件发行者证书（SPC）或 Windows 硬件质量实验室（WHQL）签名签署的代码不得方便绕过 Windows 代码完整性和安全技术。  在通过受信任的 SPC 或 WHQL 签名对代码进行签名之前，请先确保它符合[创建可靠的内核模式驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-reliable-kernel-mode-drivers)的指南。 此外，代码不得包含任何危险行为，如下所述。  有关驱动程序签名的详细信息，请参阅本文后面的[发布驱动程序签名](#releasedriversigning)。

危险行为的示例包括：

- 提供将任意内核、物理或设备内存映射到用户模式的功能。
- 提供读取或写入任意内核、物理或设备内存的功能，包括端口输入/输出（i/o）。
- 提供跳过 Windows 访问控制的存储的访问权限。
- 用于修改驱动程序设计为不管理的硬件或固件。  

## <a name="span-idthreatanalysisspanspan-idthreatanalysisspanspan-idthreatanalysisspanperform-threat-analysis"></a><span id="ThreatAnalysis"></span><span id="threatanalysis"></span><span id="THREATANALYSIS"></span>执行威胁分析

**安全清单项 \#5：** *修改现有的驱动程序威胁模型或创建自定义的驱动程序威胁模型。*

考虑到安全性，一种常见的方法是创建具体的威胁模型，以尝试描述可能的攻击类型。 设计驱动程序时，此方法非常有用，因为它会强制开发人员提前考虑潜在的攻击媒介。 如果已确定潜在的威胁，驱动程序开发人员就可以考虑防御这些威胁，从而加强驱动程序组件的总体安全性。

本文提供了有关创建轻型威胁模型的特定于驱动程序的指南：[驱动程序的威胁建模](threat-modeling-for-drivers.md)。 本文提供了一个示例驱动程序威胁模型关系图，可将其用作驱动程序的起点。

![假设内核模式驱动程序的示例数据流图表](images/sampledataflowdiagramkernelmodedriver.gif)

Ihv 和 Oem 可以使用安全开发生命周期（SDL）最佳实践和相关工具来提高产品的安全性。 有关详细信息，请参阅[适用于 oem 的 SDL 建议](https://docs.microsoft.com/windows-hardware/drivers/bringup/security-overview#sdl-recommendations-for-oems)。

## <a name="span-iddriversecuritycodepracticesspanspan-iddriversecuritycodepracticesspanspan-iddriversecuritycodepracticesspanfollow-driver-secure-coding-guidelines"></a><span id="DriverSecurityCodePractices"></span><span id="driversecuritycodepractices"></span><span id="DRIVERSECURITYCODEPRACTICES"></span>遵循驱动程序安全编码准则

**安全清单项 \#6：** *检查代码并删除任何已知的代码漏洞。*

创建安全驱动程序的核心活动是识别代码中需要更改的区域，以避免已知的软件漏洞。 其中的许多已知软件漏洞都涉及到严格跟踪内存使用情况，以避免他人覆盖或包含驱动程序使用的内存位置的问题。

本文的[代码验证工具](#codevalidationtools)部分介绍了可用于帮助查找已知软件漏洞的软件工具。

**内存缓冲区**

- 请始终检查输入缓冲区和输出缓冲区的大小，以确保缓冲区可以容纳所有请求的数据。 有关详细信息，请参阅[检查缓冲区大小失败](https://docs.microsoft.com/windows-hardware/drivers/kernel/failure-to-check-the-size-of-buffers)。

- 在将所有输出缓冲区返回给调用方之前，请正确地将其初始化为零。 有关详细信息，请参阅[初始化输出缓冲区失败](https://docs.microsoft.com/windows-hardware/drivers/kernel/failure-to-initialize-output-buffers)。

- 验证长度可变的缓冲区。 有关详细信息，请参阅[验证可变长度缓冲区失败](https://docs.microsoft.com/windows-hardware/drivers/kernel/failure-to-validate-variable-length-buffers)。 有关使用缓冲区并使用[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)和[**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)验证缓冲区的地址的详细信息，请参阅[缓冲区处理](https://docs.microsoft.com/windows-hardware/drivers/ifs/buffer-handling)。

**使用适当的方法通过 IOCTLs 访问数据缓冲区**

Windows 驱动程序的主要职责之一是在用户模式应用程序和系统设备之间传输数据。 下表显示了用于访问数据缓冲区的三种方法。

|IOCTL 缓冲区类型 | 摘要                                    | 更多相关信息 |  
|------------------|--------------------------------------------|-------------------------------------------------------------------------|
| METHOD_BUFFERED  |建议用于大多数 situtations            | [使用缓冲 i/o](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-buffered-i-o)
| METHOD_IN_DIRECT 或 METHOD_OUT_DIRECT |用于某些高速硬件 i/o    |[使用直接 i/o](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-direct-i-o) |
| METHOD_NEITHER |尽可能避免 |[不使用缓冲和直接 i/o](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-neither-buffered-nor-direct-i-o)|

建议使用一般的缓冲 i/o，因为它提供最安全的缓冲方法。 但即使使用缓冲 i/o 也存在风险，如必须缓解的嵌入指针。

有关在 IOCTLs 中使用缓冲区的详细信息，请参阅[访问数据缓冲区的方法](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)。

**对 IOCTL 缓冲 i/o 使用错误**

- 检查 IOCTL 相关缓冲区的大小。 有关详细信息，请参阅[检查缓冲区大小失败](https://docs.microsoft.com/windows-hardware/drivers/kernel/failure-to-check-the-size-of-buffers)。

- 正确初始化输出缓冲区。 有关详细信息，请参阅[初始化输出缓冲区失败](https://docs.microsoft.com/windows-hardware/drivers/kernel/failure-to-initialize-output-buffers)。

- 正确验证长度可变的缓冲区。 有关详细信息，请参阅[验证可变长度缓冲区失败](https://docs.microsoft.com/windows-hardware/drivers/kernel/failure-to-validate-variable-length-buffers)。

- 使用缓冲 i/o 时，请确保并在[IO_STATUS_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构信息字段中为 OutputBuffer 返回正确的长度。  不要直接从读取请求直接返回长度。  例如，假设有这样一种情况：用户空间返回的数据指示存在4K 缓冲区。  如果驱动程序实际只应返回200字节，而只是在信息字段中返回4K，则会出现信息泄漏漏洞。 出现此问题的原因在于，在 Windows 的早期版本中，i/o 管理器用于缓冲 i/o 的缓冲区未归零。  这样，用户应用将返回原始的200字节的数据，以及缓冲区中的数据的 4K-200 字节（非分页池内容）。 这种情况可能发生在所有使用缓冲 i/o 的情况下，而不只是与 IOCTLs 一起使用。

**IOCTL 直接 i/o 中的错误**

正确处理长度为零的缓冲区。 有关详细信息，请参阅[直接 i/o 中的错误](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-direct-i-o)。

**引用用户空间地址时出错**

- 验证嵌入在缓冲 i/o 请求中的指针。 有关详细信息，请参阅[引用用户空间地址中的错误](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)。

- 在尝试使用用户空间中的任何地址之前，请使用[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)和[**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)之类的 api （如果适用）。

**TOCTOU 漏洞**

使用直接 i/o （适用于 IOCTLs 或读/写）时，可能会出现检查时间（TOCTOU）漏洞的[可能时间](https://en.wikipedia.org/wiki/Time_of_check_to_time_of_use)。  请注意，驱动程序正在访问用户数据缓冲区，用户可以同时访问它。

若要管理此风险，请将需要验证的所有参数从用户数据缓冲区复制到仅从内核模式（如堆栈或池）中 accessibly 的内存。  然后，用户应用程序无法访问数据后，验证并操作传入的数据。

**驱动程序代码必须正确使用内存**

- 所有驱动程序池分配都必须位于不可执行的（NX）池中。 使用 NX 内存池本质上比使用可执行非分页（NP）池更安全，并提供更好的保护来防范溢出攻击。

- 设备驱动程序必须正确处理各种用户模式，以及内核到内核 i/o 和请求。

若要允许驱动程序支持要求 HVCI 虚拟化，需要额外的内存。 有关详细信息，请参阅本文后面的[Device Guard 兼容性](#dgc)。

**手柄**

- 验证在用户模式和内核模式内存之间传递的句柄。 有关详细信息，请参阅[处理管理](https://docs.microsoft.com/windows-hardware/drivers/ifs/handle-management)和[验证对象句柄失败](https://docs.microsoft.com/windows-hardware/drivers/kernel/failure-to-validate-object-handles)。

**设备对象**

- 保护设备对象。 有关详细信息，请参阅[保护设备对象](https://docs.microsoft.com/windows-hardware/drivers/kernel/securing-device-objects)。

- 验证设备对象。 有关详细信息，请参阅[无法验证设备对象](https://docs.microsoft.com/windows-hardware/drivers/kernel/failure-to-validate-device-objects)。

**Irp**

**WDF 和 Irp**

使用 WDF 的一个优点是，WDF 驱动程序通常不会直接访问 Irp。 例如，框架将表示读取、写入和设备 i/o 控制操作的 WDM Irp 转换为在 i/o 队列中 KMDF/UMDF 接收的框架请求对象。

如果要编写 WDM 驱动程序，请查看以下指南。

**正确管理 IRP i/o 缓冲区**

以下文章提供了有关验证 IRP 输入值的信息：

[使用缓冲 i/o 的 DispatchReadWrite](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchreadwrite-using-buffered-i-o)

[缓冲 i/o 中的错误](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-buffered-i-o)

[使用直接 i/o 的 DispatchReadWrite](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchreadwrite-using-direct-i-o)

[直接 i/o 中的错误](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-direct-i-o)

[I/o 控制代码的安全问题](https://docs.microsoft.com/windows-hardware/drivers/kernel/security-issues-for-i-o-control-codes)

请考虑验证与 IRP 关联的值，例如缓冲区地址和长度。

如果你选择不使用 i/o，请注意，与读取和写入不同，与缓冲 i/o 和直接 i/o 不同，在使用 i/o IOCTL 时，i/o 管理器不会验证缓冲区指针和长度。  

**正确处理 IRP 完成操作**

驱动程序永远不能完成状态值为 STATUS 的 IRP\_SUCCESS，除非它实际支持和处理 IRP。 有关处理 IRP 完成操作的正确方法的信息，请参阅[完成 irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/completing-irps)。

**管理驱动程序 IRP 挂起状态**

驱动程序在保存 IRP 之前应将 IRP 标记为 "挂起"，并且应考虑同时包含对[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)的调用和互锁序列中的分配。 有关详细信息，请参阅[在设备暂停时](https://docs.microsoft.com/windows-hardware/drivers/kernel/holding-incoming-irps-when-a-device-is-paused)[检查驱动程序的状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/failure-to-check-a-driver-s-state)并保存传入的 irp。

**正确处理 IRP 取消操作**

取消操作很难正确编码，因为它们通常以异步方式执行。 处理取消操作的代码中的问题可能会很长时间被忽略，因为通常不会在运行的系统中频繁执行此代码。 务必阅读并了解[取消 irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/canceling-irps)下提供的所有信息。 [在取消 Irp 时，请](https://docs.microsoft.com/windows-hardware/drivers/kernel/points-to-consider-when-canceling-irps)特别注意[同步 IRP 取消](https://docs.microsoft.com/windows-hardware/drivers/kernel/synchronizing-irp-cancellation)和要考虑的事项。

最大程度地减少与取消操作关联的同步问题的一种建议方法是实现[取消安全 IRP 队列](https://docs.microsoft.com/windows-hardware/drivers/kernel/cancel-safe-irp-queues)。

**正确处理 IRP 清理并关闭操作**

请确保了解[**IRP\_mj\_清理**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)和[**irp\_MJ\_关闭**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)请求之间的差异。 清理请求在应用程序关闭文件对象上的所有句柄之后，但有时在所有 i/o 请求完成之前到达。 完成或取消对文件对象的所有 i/o 请求后，关闭请求即可到达。 有关详细信息，请参阅以下文章：

[DispatchCreate、DispatchClose 和 DispatchCreateClose 例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchcreate--dispatchclose--and-dispatchcreateclose-routines)

[DispatchCleanup 例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchcleanup-routines)

[处理清理和关闭操作时出错](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-handling-cleanup-and-close-operations)

有关正确处理 Irp 的详细信息，请参阅[处理 irp 中的其他错误](https://docs.microsoft.com/windows-hardware/drivers/kernel/additional-errors-in-handling-irps)。

**其他安全问题**

- 使用锁定或联锁序列来防止争用条件。 有关详细信息，请参阅[多处理器环境中的错误](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-a-multiprocessor-environment)。

- 确保设备驱动程序能够正确处理各种用户模式以及内核 i/o 请求。

- 确保在安装或使用过程中，驱动程序或未安装 TDI 筛选器或 Lsp。

**使用安全函数**

- 使用安全字符串函数。 有关详细信息，请参阅[使用安全字符串函数](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-safe-string-functions)。

- 使用安全算术函数。 有关详细信息，请参阅[安全整数库例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)中的[算术函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

- 使用安全转换函数。 有关详细信息，请参阅[安全整数库例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)中的[转换函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

**其他代码漏洞**

除了本文所述的可能的漏洞之外，本文还提供了有关增强内核模式驱动程序代码的安全性的其他信息：[创建可靠的内核模式驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-reliable-kernel-mode-drivers)。

有关 C 和C++安全编码的其他信息，请参阅本文末尾的[安全编码资源](#securecodingresources)。



## <a name="span-idmanagingdriveraccesscontrolspanspan-idmanagingdriveraccesscontrolspanspan-idmanagingdriveraccesscontrolspanmanage-driver-access-control"></a><span id="ManagingDriverAccessControl"></span><span id="managingdriveraccesscontrol"></span><span id="MANAGINGDRIVERACCESSCONTROL"></span>管理驱动程序访问控制

**安全清单项 \#7：** *检查您的驱动程序以确保正确控制访问。*

**管理驱动程序访问控制-WDF**

驱动程序必须工作，以防止用户不正当地访问计算机的设备和文件。 若要防止对设备和文件进行未经授权的访问，你必须：

- 仅在必要时命名设备对象。 命名设备对象通常只是出于传统原因所必需的，例如，如果应用程序需要使用特定的名称打开设备，或者使用非 PNP 设备/控制设备。  请注意，WDF 驱动程序无需命名它们的 PnP 设备 FDO 即可使用[WdfDeviceCreateSymbolicLink](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatesymboliclink)创建符号链接。

- 安全访问设备对象和接口。

为了使应用程序或其他 WDF 驱动程序能够访问 PnP 设备 PDO，你应该使用设备接口。 有关详细信息，请参阅[使用设备接口](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-device-interfaces)。 设备接口用作设备堆栈 PDO 的符号链接。

控制 PDO 访问权限的举世无双方法之一是在 INF 中指定一个 SDDL 字符串。 如果 SDDL 字符串不在 INF 文件中，则 Windows 将应用默认安全描述符。 有关详细信息，请参阅[为设备](https://docs.microsoft.com/windows-hardware/drivers/kernel/sddl-for-device-objects)对象[保护设备对象](https://docs.microsoft.com/windows-hardware/drivers/kernel/securing-device-objects)和 SDDL。

有关控制访问的详细信息，请参阅以下文章：

[在 KMDF 驱动程序中控制设备访问](https://docs.microsoft.com/windows-hardware/drivers/wdf/controlling-device-access-in-kmdf-drivers)

[名称、安全描述符和设备类-使设备对象可访问 。](https://www.osr.com/nt-insider/2017-issue1/making-device-objects-accessible-safe/)从*2017 年1月1日起*， [OSR](https://www.osr.com)发布的 NT 有问必答新闻稿。

**管理驱动程序访问控制-WDM**

如果使用的是 WDM 驱动程序，并且使用的是命名设备对象，则可以使用[IoCreateDeviceSecure](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)并指定 SDDL 来保护它。 实现[IoCreateDeviceSecure](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)时，请始终指定 DeviceClassGuid 的自定义类 GUID。 不应在此指定现有的类 GUID。 这样做可能会中断属于该类的其他设备的安全设置或兼容性。 有关详细信息，请参阅[WdmlibIoCreateDeviceSecure](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)。

有关详细信息，请参阅以下文章：

[控制设备访问](https://docs.microsoft.com/windows-hardware/drivers/kernel/controlling-device-access)

[控制设备命名空间访问](https://docs.microsoft.com/windows-hardware/drivers/kernel/controlling-device-namespace-access)

[适用于驱动程序开发人员的 Windows 安全模型](windows-security-model.md)

**安全标识符（Sid）风险层次结构**

以下部分介绍了驱动程序代码中使用的常见 Sid 的风险层次结构。 有关 SDDL 的一般信息，请参阅[sddl 了解设备对象](https://docs.microsoft.com/windows-hardware/drivers/kernel/sddl-for-device-objects)、 [SID 字符串](https://docs.microsoft.com/windows/desktop/SecAuthZ/sid-strings)和[sddl 字符串语法](https://docs.microsoft.com/openspecs/windows_protocols/ms-dtyp/f4296d69-1c0f-491f-9587-a960b292d070)。

必须了解，如果允许较低权限调用方访问内核，则会增加代码风险。 在此摘要图中，当你允许低权限 Sid 访问驱动程序功能时，风险会增加。

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

按照一般最低权限安全原则，仅配置驱动程序运行所需的最低访问级别。

**WDM 精细 IOCTL 安全控制**

为了进一步管理用户模式调用方发送 IOCTLs 时的安全性，驱动程序代码可以包括[IoValidateDeviceIoControlAccess](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iovalidatedeviceiocontrolaccess)函数。 此函数允许驱动程序检查访问权限。 接收 IOCTL 后，驱动程序可以调用[IoValidateDeviceIoControlAccess](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iovalidatedeviceiocontrolaccess)，同时指定 FILE_READ_ACCESS、FILE_WRITE_ACCESS 或两者。

实现精细的 IOCTL 安全控制不会取代使用上述技术来管理驱动程序访问的需要。

有关详细信息，请参阅以下文章：

[定义 i/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)

## <a name="span-iddgcspanspan-iddgcspanvalidate-device-guard-compatibility"></a><span id="DGC"></span><span id="dgc"></span>验证 Device Guard 兼容性

**安全清单项 \#8：** *验证驱动程序是否使用内存，使其与设备保护兼容。*

**内存使用情况和设备防护兼容性**

Device Guard 使用硬件技术和虚拟化将代码完整性（CI）决策函数与操作系统的其余部分隔离开来。 使用基于虚拟化的安全性隔离 CI 时，内核内存可执行的唯一方式是通过 CI 验证。 这意味着内核内存页永远不能为可写且可执行（W + X）和可执行代码不能直接修改。

若要实现 Device Guard 兼容的代码，请确保你的驱动程序代码执行以下操作：

- 默认情况下，使用 NX
- 使用 NX Api/标志进行内存分配（NonPagedPoolNx）
- 不使用可写和可执行的节
- 不尝试直接修改可执行系统内存
- 不使用内核中的动态代码
- 不将数据文件加载为可执行文件
- 节对齐方式为0x1000 的倍数（页\_大小）。 例如 驱动程序\_对齐 = 0x1000

若要详细了解如何使用该工具和不兼容的内存调用列表，请参阅[使用设备保护准备工具评估要求 hvci 驱动程序兼容性](use-device-guard-readiness-tool.md)。

有关 Device Guard 的一般信息，请参阅[Windows 10 中与设备保护的驱动程序兼容性](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)。

有关相关系统基础安全测试的详细信息，请参阅[设备保护性测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/10c242b6-49f6-491d-876c-c39b22b36abc)和[与设备保护的驱动程序兼容性](https://docs.microsoft.com/windows-hardware/test/hlk/testref/driver-compatibility-with-device-guard)。

## <a name="span-idtechnologyspecificcodepracticesspanfollow-technology-specific-code-best-practices"></a><span id="technologyspecificcodepractices"></span>遵循特定于技术的代码最佳做法

**安全清单项 \#9：** *查看适用于你的驱动程序的以下特定于技术的指南。*

*文件系统*

有关详细信息，请参阅以下文章：

[文件系统的安全注意事项](https://docs.microsoft.com/windows-hardware/drivers/ifs/security-considerations-for-file-systems)

[文件系统安全问题](https://docs.microsoft.com/windows-hardware/drivers/ifs/file-system-security-issues)

[文件系统的安全功能](https://docs.microsoft.com/windows-hardware/drivers/ifs/security-features-for-file-systems)

[文件系统筛选器驱动程序的安全注意事项](https://docs.microsoft.com/windows-hardware/drivers/ifs/security-considerations-for-file-system-filter-drivers)

*NDIS-网络*

有关 NDIS 驱动程序安全的信息，请参阅[网络驱动程序的安全问题](https://docs.microsoft.com/windows-hardware/drivers/network/security-issues-for-network-drivers)。

*显示器*

有关显示驱动程序安全性的信息，请参阅 &lt;内容挂起&gt;。

*Printers*

有关打印机驱动程序安全的信息，请参阅[V4 打印机驱动程序安全注意事项](https://docs.microsoft.com/windows-hardware/drivers/print/v4-printer-driver-security-considerations)。

*Windows 图像获取（WIA）驱动程序的安全问题*

有关 WIA 安全性的信息，请参阅[Windows 图像获取（WIA）驱动程序的安全问题](https://docs.microsoft.com/windows-hardware/drivers/image/security-issues-for-wia-drivers)。

## <a name="span-idenhancedeviceinstallationsecurityspanenhance-device-installation-security"></a><span id="enhancedeviceinstallationsecurity"></span>增强设备安装安全性

**安全清单项 \#10：** *查看驱动程序 inf 创建和安装指南，确保遵循最佳做法。*

当你创建用于安装驱动程序的代码时，必须确保始终以安全的方式执行你的设备安装。 安全设备安装是指执行以下操作的设备：

- 限制对设备及其设备接口类的访问
- 限制对为设备创建的驱动程序服务的访问权限
- 保护驱动程序文件不被修改或删除
- 限制对设备的注册表项的访问
- 限制对设备的 WMI 类的访问
- 正确使用 Setupapi.log 函数

有关详细信息，请参阅以下文章：

[创建安全设备安装](https://docs.microsoft.com/windows-hardware/drivers/install/creating-secure-device-installations)

[使用 Setupapi.log 的准则](https://docs.microsoft.com/windows-hardware/drivers/install/guidelines-for-using-setupapi)

[使用设备安装功能](https://docs.microsoft.com/windows-hardware/drivers/install/using-device-installation-functions)

[设备和驱动程序安装高级主题](https://docs.microsoft.com/windows-hardware/drivers/install/device-and-driver-installation-advanced-topics)

## <a name="span-idpeercodereviewspanperform-peer-code-review"></a><span id="peercodereview"></span>执行对等代码评审

**安全清单项 \#11：** *执行对等代码评审，以查找其他工具和进程未出现的问题*

寻找熟悉的代码审阅者，查找可能丢失的问题。 另一组眼睛通常会发现可能已被忽略的问题。

如果你没有适当的员工在内部查看代码，请考虑为此目的提供外部帮助。

## <a name="span-idreleasedriversigningspanspan-idreleasedriversigningspanspan-idreleasedriversigningspanexecute-proper-release-driver-signing"></a><span id="ReleaseDriverSigning"></span><span id="releasedriversigning"></span><span id="RELEASEDRIVERSIGNING"></span>执行正确的发布驱动程序签名

**安全核对清单项 \#12：** *使用 Windows 合作伙伴门户对驱动程序进行正确签名以进行分发。*

在公开发布驱动程序包之前，我们建议你先提交程序包以进行认证。 有关详细信息，请参阅对[性能和兼容性进行测试](https://docs.microsoft.com/windows-hardware/test/index)，[开始使用硬件计划](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-started-with-the-hardware-dashboard)、[硬件仪表板服务](https://docs.microsoft.com/windows-hardware/drivers/dashboard/dashboard-services)以及使用[公共发布的内核驱动程序进行签名](https://docs.microsoft.com/windows-hardware/drivers/dashboard/attestation-signing-a-kernel-driver-for-public-release)。

## <a name="span-iduse-code-analysisspanuse-code-analysis-in-visual-studio-to-investigate-driver-security"></a><span id="use-code-analysis"></span>在 Visual Studio 中使用代码分析来调查驱动程序安全性

**安全清单项 \#13：** *请按照以下步骤使用 Visual Studio 中的代码分析功能来检查驱动程序代码中的漏洞。*

使用 Visual Studio 中的代码分析功能来检查代码中的安全漏洞。 Windows 驱动程序工具包（WDK）安装旨在检查本机驱动程序代码中的问题的规则集。

有关详细信息，请参阅[如何对驱动程序运行代码分析](https://docs.microsoft.com/windows-hardware/drivers/devtest/how-to-run-code-analysis-for-drivers)。

有关详细信息，请参阅[驱动程序代码分析概述](https://docs.microsoft.com/windows-hardware/drivers/devtest/code-analysis-for-drivers-overview)。 有关代码分析的更多背景知识，请参阅[深层 Visual Studio 2013 静态代码分析](https://blogs.msdn.microsoft.com/hkamel/2013/10/24/visual-studio-2013-static-code-analysis-in-depth-what-when-and-how/)。

若要熟悉代码分析，可以使用其中一个示例驱动程序，例如，<https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster/toastDrv/kmdf/func/featured> toaster 或 ELAM 初期启动反恶意软件示例 <https://github.com/Microsoft/Windows-driver-samples/tree/master/security/elam>。

1. 在 Visual Studio 中打开驱动程序解决方案。

2. 在 Visual Studio 中，对于解决方案中的每个项目，将项目属性更改为使用所需的规则集。 例如：项目 &gt;&gt; 属性 &gt;&gt; 代码分析 &gt;&gt; 常规 "，请选择"*推荐的驱动程序规则*"。 除了使用 recommenced 驱动程序规则之外，还可以使用 "*建议的本机规则*" 规则集。

3. 选择 "生成" &gt;&gt; 对解决方案运行代码分析。

4. 在 Visual Studio 中的 "生成输出" 窗口的 "**错误列表**" 选项卡中查看警告。

单击每个警告的说明，以查看代码中有问题的区域。

单击链接的警告代码可查看其他信息。

确定是否需要更改你的代码，或者是否需要添加批注以允许代码分析引擎正确遵循你的代码的意图。 有关代码批注的详细信息，请参阅[使用 SAL 注释减少 C/C++代码缺陷](https://docs.microsoft.com/visualstudio/code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects?view=vs-2015)和[用于 Windows 驱动程序的 SAL 2.0 批注](https://docs.microsoft.com/windows-hardware/drivers/devtest/sal-2-annotations-for-windows-drivers)。

有关 SAL 的一般信息，请参阅 OSR 中的这篇文章。
[https://www.osr.com/blog/2015/02/23/sal-annotations-dont-hate-im-beautiful/](https://www.osr.com/blog/2015/02/23/sal-annotations-dont-hate-im-beautiful/)

## <a name="span-idsdvspanspan-idsdvspanuse-static-driver-verifier-to-check-for-vulnerabilities"></a><span id="SDV"></span><span id="sdv"></span>使用静态驱动程序验证程序检查是否存在漏洞

**安全核对清单项 \#14：** *按照以下步骤使用 Visual Studio 中的静态驱动程序验证程序（SDV）检查驱动程序代码中的漏洞。*

静态驱动程序验证程序（SDV）使用一组接口规则和操作系统模型来确定驱动程序是否与 Windows 操作系统正确交互。 SDV 在驱动程序代码中查找一些缺陷，这些缺陷可能指向驱动程序中的潜在 bug。

有关详细信息，请参阅[静态驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/introducing-static-driver-verifier)和[静态驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)简介。 请注意，SDV 仅支持某些类型的驱动程序。 有关 SDV 可以验证的驱动程序的详细信息，请参阅[支持的驱动程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/supported-drivers)。

若要熟悉 SDV，可以使用其中一个示例驱动程序（例如，特色 toaster 示例： <https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster/toastDrv/kmdf/func/featured>）。

1. 在 Visual Studio 中打开目标驱动程序解决方案。

2. 在 Visual Studio 中，将生成类型更改为 "*发布*"。 静态驱动程序验证程序要求生成类型为 release，而不是调试。

3. 在 Visual Studio 中，选择 "生成" &gt;&gt; 生成解决方案 "。

4. 在 Visual Studio 中，选择 "驱动程序" &gt;&gt; 启动静态驱动程序验证程序 "。

5. 在 SDV 的 "*规则*" 选项卡上，选择 "*规则集*" 下的 "*默认*"。

尽管默认规则发现许多常见问题，但也请考虑运行更全面的 "*所有驱动程序规则*" 规则集。

6. 在 SDV 的*主*选项卡上，单击 "*启动*"。

7. 当 SDV 完成时，查看输出中的任何警告。 *主*选项卡显示发现的缺陷总数。

8. 单击每个警告以加载 "SDV 报表" 页，并检查与可能的代码漏洞关联的信息。 使用报表调查验证结果，并确定驱动程序中 SDV 验证失败的路径。 有关详细信息，请参阅[静态驱动程序验证程序报表](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier-report)。

## <a name="span-idbinscopespanspan-idbinscopespanspan-idbinscopespancheck-code-with-binscope-binary-analyzer"></a><span id="BinScope"></span><span id="binscope"></span><span id="BINSCOPE"></span>用 BinScope 二进制分析器检查代码

**安全清单项 \#15：** *请按照以下步骤进行操作，以使用 BinScope 来仔细检查是否配置了编译和生成选项，以最大程度地减少已知的安全问题。*

使用 BinScope 来检查应用程序的二进制文件，以确定编码和构建方法，这可能会导致应用程序容易受到攻击或用作攻击向量。

有关详细信息，请参阅[新版 BinScope 二进制分析器](https://www.microsoft.com/security/blog/2014/11/20/new-binscope-released/)以及该工具下载中附带的用户和入门指南。

按照以下步骤验证是否已在你要发货的代码中正确配置了安全编译选项：

1. 从此处下载 BinScope Analyzer 和相关文档： <https://www.microsoft.com/download/details.aspx?id=44995>。

2. 查看下载的*BinScope 入门指南*。

3. 使用 MSI 文件在目标测试计算机上安装 BinScope，其中包含要验证的已编译代码。

4. 打开命令提示符窗口，并执行以下命令以检查已编译的驱动程序二进制文件。 将路径更新为指向你编译的驱动程序 sys.databases 文件。

```cpp
C:\Program Files\Microsoft BinScope 2014>binscope "C:\Samples\KMDF_Echo_Driver\echo.sys" /verbose /html /logfile c:\mylog.htm
```

5. 使用浏览器查看 BinScope 报表，以确认所有检查标记为（通过）。

默认情况下，HTML 报表将写入 \\用户\\&lt;用户名&gt;\\BinScope\\

有三个类别可能输出到一个日志文件中：

- 失败的检查 \[失败\]
- 检查未完成 \[错误\]
- 传递的检查 \[Pass\]

请注意，传递的检查在默认情况下不会写入日志，并且必须通过使用/verbose 开关来启用。

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

**安全清单项 \#16：** *使用这些附加工具来帮助验证你的代码是否遵循安全建议，并探测你的开发过程中丢失的空白。*

除了上面所述[Visual Studio Code 分析](#use-code-analysis)、[静态驱动程序验证程序](#sdv)和[Binscope](#binscope) ，还可以使用以下工具来探测开发过程中丢失的缺口。

**驱动程序验证程序**

驱动程序验证程序允许对驱动程序进行实时测试。 驱动程序验证程序监视 Windows 内核模式驱动程序和图形驱动程序，目的是检测可能损坏系统的非法函数调用或操作。 驱动程序验证程序可将 Windows 驱动程序用于各种强调和测试，以找出不正确的行为。 有关详细信息，请参阅[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)。

**硬件兼容性计划测试**

硬件兼容性程序包含安全相关的测试，可用于查找代码漏洞。 Windows 硬件兼容性计划利用 Windows 硬件实验室工具包（HLK）中的测试。 可以在命令行上使用 HLK 设备基础测试来运用驱动程序代码和探测漏洞。 有关设备基础测试和硬件兼容性计划的一般信息，请参阅[Windows 硬件实验室工具包](https://docs.microsoft.com/windows-hardware/test/hlk/)。

以下测试是检查与代码漏洞相关的某些行为的驱动程序代码可能很有用的测试示例：

 [DF - 模糊随机 IOCTL 测试（可靠性）](https://docs.microsoft.com/windows-hardware/test/hlk/testref/236b8ad5-0ba1-4075-80a6-ae9dafb71c94)

 [DF - 模糊 sub-open 测试（可靠性）](https://docs.microsoft.com/windows-hardware/test/hlk/testref/92bf534e-aa48-4aeb-b3cd-e46fb7cc7d80)

 [DF - 模糊零长度缓冲区 FSCTL 测试（可靠性）](https://docs.microsoft.com/windows-hardware/test/hlk/testref/5f5f6c7e-d5db-4ff1-8cee-da47203ab070)

 [DF - 模糊随机 FSCTL 测试（可靠性）](https://docs.microsoft.com/windows-hardware/test/hlk/testref/e529e34e-076a-4978-926f-7eca333e8f4d)

 [DF - 模糊杂项 API 测试（可靠性）](https://docs.microsoft.com/windows-hardware/test/hlk/testref/fb305d04-6e8c-4dfc-9984-9692df82fbd8)

 你还可以使用驱动程序验证程序附带的[内核同步延迟模糊](https://docs.microsoft.com/windows-hardware/drivers/devtest/kernel-synchronization-delay-fuzzing)处理。

混乱（并发硬件和操作系统）测试会同时运行各种 PnP 驱动程序测试、设备驱动程序模糊测试和电源系统测试。 有关详细信息，请参阅[混乱的测试（设备基础）](https://docs.microsoft.com/windows-hardware/drivers/devtest/chaos-tests--device-fundamentals-)。

设备基础的渗透测试执行各种形式的输入攻击，这是安全测试的关键组成部分。 攻击和渗透测试可帮助识别软件接口中的漏洞。 有关详细信息，请参阅[渗透测试（设备基础）](https://docs.microsoft.com/windows-hardware/drivers/devtest/penetration-tests--device-fundamentals-)。

使用[Device Guard 合规性测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/10c242b6-49f6-491d-876c-c39b22b36abc)以及本文中所述的其他工具，以确认您的驱动程序与 Device Guard 兼容。

**自定义和域特定的测试工具**

考虑开发自定义域特定的安全测试。 要开发其他测试，请从该软件的原始设计器中收集输入，以及熟悉正在开发的特定驱动程序类型的无关开发资源，以及一个或多个熟悉安全入侵分析和措施.

## <a name="span-iddebuggerspanspan-iddebuggerspanspan-iddebuggerspanreview-debugger-techniques-and-extensions"></a><span id="Debugger"></span><span id="debugger"></span><span id="DEBUGGER"></span>查看调试器技术和扩展

**安全清单项 \#17：** *查看这些调试器工具并考虑它们在开发调试工作流中的使用。*

**！可利用故障分析器**

！可利用的故障分析器是一种 Windows 调试程序扩展，用于分析查找独特问题的崩溃日志。 它还检查崩溃类型，并尝试确定错误是否是恶意黑客可以利用的问题。

Microsoft 安全工程中心（毫秒），创建了！可利用故障分析器。 可以从 codeplex 下载： <https://msecdbg.codeplex.com/>。

有关详细信息，请参阅[！可利用的崩溃分析器版本 1.6](https://www.microsoft.com/security/blog/2013/06/13/exploitable-crash-analyzer-version-1-6/)和第9频道视频[！可利用故障分析器](https://channel9.msdn.com/blogs/pdcnews/bang-exploitable-security-analyzer)。

**与安全性相关的调试器命令**

！ Acl 扩展格式化并显示访问控制列表（ACL）的内容。 有关详细信息，请参阅[确定对象的 ACL](https://docs.microsoft.com/windows-hardware/drivers/debugger/determining-the-acl-of-an-object)和[ **！ acl**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-acl)。

！令牌扩展显示安全令牌对象的格式化视图。 有关详细信息，请参阅[ **！ token**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-token)。

！ Tokenfields extension 显示访问令牌对象（令牌结构）中的字段的名称和偏移量。 有关详细信息，请参阅[ **！ tokenfields**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-tokenfields)。

！ Sid 扩展显示指定地址处的安全标识符（SID）。 有关详细信息，请参阅[ **！ sid**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-sid)。

！ Sd extension 显示指定地址处的安全描述符。 有关详细信息，请参阅[ **！ sd**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-sd)。

## <a name="span-idsecurecodingresourcesspanspan-idsecurecodingresourcesspanspan-idsecurecodingresourcesspanreview-secure-coding-resources"></a><span id="SecureCodingResources"></span><span id="securecodingresources"></span><span id="SECURECODINGRESOURCES"></span>查看安全编码资源

**安全核对清单项 \#18：** *查看这些资源，以扩展对驱动程序开发人员适用的安全编码最佳实践的了解。*

*查看这些资源，了解有关驱动程序安全性的详细信息*

**保护内核模式驱动程序编码准则**

[创建可靠的内核模式驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-reliable-kernel-mode-drivers)

**安全编码组织**

[Carnegie 卡内基梅隆大学 SEI 证书](https://www.sei.cmu.edu/about/divisions/cert/index.cfm)

Carnegie 卡内基梅隆大学 SEI CERT [C 编码标准：用于开发安全、可靠和安全系统](https://www.securecoding.cert.org/confluence/display/c/SEI+CERT+C+Coding+Standard)（2016版）的规则。

CERT-[生成安全性](https://www.us-cert.gov/bsi)

MITRE-[由 CERT C 安全编码标准解决的漏洞](https://cwe.mitre.org/data/definitions/734.html)

在成熟度模型中构建安全性（BSIMM）- [https://www.bsimm.com/](https://www.bsimm.com/)

SAFECode- [https://safecode.org/](https://safecode.org/)

**OSR**

[OSR](https://www.osr.com)提供驱动程序开发培训和咨询服务。 OSR 新闻稿中的这些文章突出显示了驱动程序安全问题。

[名称、安全描述符和设备类-使设备对象可访问 。和安全](https://www.osr.com/nt-insider/2017-issue1/making-device-objects-accessible-safe/)

[已走使用保护--内部驱动程序 & 设备安全](https://www.osronline.com/article.cfm^article=100.htm)

[锁定驱动程序-技术调查](https://www.osronline.com/article.cfm^article=357.htm)

[Meltdown 和 Spectre：驱动程序？](https://www.osr.com/blog/2018/01/23/meltdown-spectre-drivers/)

**案例研究**

[从警报到驱动程序漏洞： Microsoft Defender ATP 调查 unearths 特权升级缺陷](https://www.microsoft.com/security/blog/2019/03/25/from-alert-to-driver-vulnerability-microsoft-defender-atp-investigation-unearths-privilege-escalation-flaw/)

**帐簿**

*24 抱问题软件安全：* Michael Howard、David LeBlanc 和 John Viega 的编程缺陷和解决方法

*软件安全评估的内容：识别和预防软件漏洞*，将 Dowd、John 麦克唐纳和 Justin Schuh

*编写安全软件 Second Edition*、Michael Howard 和 David LeBlanc

*软件安全评估的内容：识别并防止软件漏洞*，将 Dowd 和约翰麦克唐纳

*C 和C++中的安全编码（软件工程中的 SEI 系列）第2版*，Robert Seacord

*编程 Microsoft Windows 驱动模型（第2版）* ，Walter Oney

*开发包含 Windows Driver Foundation （开发人员参考）* 、Orwick 和专家 Smith 的驱动程序

**方面**

可从以下供应商获取 Windows 驱动程序课堂培训：

- [OSR](https://www.osr.com)
- [Winsider](https://www.windows-internals.com/)
- [Azius](https://azius.com/)

可从各种源获取安全编码在线培训。 例如，可以从 coursera 获取此课程：

[https://www.coursera.org/learn/software-security](https://www.coursera.org/learn/software-security)。

SAFECode 还提供免费的培训：

[SAFECode.org/training](https://safecode.org/training/)

**专业认证**

 CERT 提供[安全的编码专业证书](https://www.sei.cmu.edu/education-outreach/credentials/index.cfm)。

## <a name="span-idkeytakeawaysspansummary-of-key-takeaways"></a><span id="keytakeaways"></span>要点总结

驱动程序安全性是包含许多元素的复杂任务，但以下是一些需要考虑的要点：

- Windows 内核中的驱动程序在内核中执行时会出现问题。 因此，请密切注意驱动程序安全性和设计，并考虑安全性。

- 应用最小特权原则：

    a. 使用 strict SDDL 字符串限制对驱动程序的访问

    b. 进一步限制单个 IOCTL 的

- 创建威胁模型来识别攻击向量，并考虑是否可以进一步限制任何内容。
- 请注意从 usermode 传入的嵌入式指针。 需要在除之外的 "try" 中对其进行探测和访问，并且它们容易出现检查时间（ToCToU）问题的时间，除非捕获和比较缓冲区的值。
- 如果不确定，请使用 METHOD_BUFFERED 作为 IOCTL 缓冲方法。
- 使用代码扫描实用程序查找已知的代码漏洞并修正任何确定的问题。
- 寻找熟悉的代码审阅者，查找可能丢失的问题。
- 使用驱动程序验证程序并使用多个输入（包括拐角情况）测试驱动程序。

[向 Microsoft 发送有关本文的注释](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[hw_design/hw_design]:%20Driver%20security%20checklist%20%20RELEASE:%20%286/16/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20 https://privacy.microsoft.com/default.aspx. "向 Microsoft 发送有关本主题的注释")

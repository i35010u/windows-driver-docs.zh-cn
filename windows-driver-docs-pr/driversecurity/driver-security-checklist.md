---
title: 驱动程序安全清单
description: 本文为驱动程序开发人员提供了驱动程序安全核对清单。
ms.assetid: 25375E02-FCA1-4E94-8D9A-AA396C909278
ms.date: 03/13/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7772f3866fdc6851ced73ccf2c5c07ce5e61504c
ms.sourcegitcommit: 1690ad77580a2cfc47debb9751fd109a5991dd52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345937"
---
# <a name="driver-security-checklist"></a>驱动程序安全清单

本文为驱动程序开发人员提供了驱动程序安全清单，以帮助降低驱动程序被泄露的风险。

## <a name="driver-security-overview"></a>驱动程序安全性概述

安全漏洞是指允许攻击者导致驱动程序故障的任何缺陷，使系统崩溃或变得不可用。 此外，驱动程序代码中的漏洞可能允许攻击者获取对内核的访问权限，从而可能危及整个操作系统的安全。 当大多数开发人员处理其驱动程序时，其重点是使驱动程序正常工作，而不是恶意攻击者是否会尝试利用其代码中的漏洞。

但是，在释放驱动程序后，攻击者可能会尝试探测并识别安全漏洞。 开发人员必须在设计和实施阶段考虑这些问题，以最大程度地减少此类漏洞的可能性。 目标是在驱动程序发布之前消除所有已知的安全漏洞。

创建更安全的驱动程序需要将系统架构师 (特意考虑到对驱动程序的潜在威胁) 、实现代码的开发人员 (对可能成为攻击) 来源的常见操作进行编码，而测试团队 (主动尝试查找的弱点和漏洞。 通过适当地协调所有这些活动，驱动程序的安全性大大增强。

除了避免与受攻击的驱动程序相关的问题，所述的许多步骤（如更精确地使用内核内存）也会提高驱动程序的可靠性。 这将降低支持成本，并提高客户对产品的满意度。 完成以下清单中的任务可帮助实现所有这些目标。

**安全清单：** *完成其中每个主题中所述的安全任务。*

![空复选框](images/checkbox.png)[确认需要内核驱动程序](#confirm-that-a-kernel-driver-is-required)

![空复选框](images/checkbox.png)[使用驱动程序框架](#use-the-driver-frameworks)

![空复选框](images/checkbox.png)[控制对仅软件驱动程序的访问](#control-access-to-software-only-drivers)

![空复选框，不](images/checkbox.png)[生产符号测试驱动程序代码](#do-not-production-sign-test-code)

![空复选框](images/checkbox.png)[执行威胁分析](#perform-threat-analysis)

![空复选框](images/checkbox.png)[遵照驱动程序安全编码准则](#follow-driver-secure-coding-guidelines)

![空复选框](images/checkbox.png)[验证要求 hvci 兼容性](#validate-hvci-compatibility)

![空复选框](images/checkbox.png)[遵循特定于技术的代码最佳做法](#follow-technology-specific-code-best-practices)

![空复选框](images/checkbox.png)[执行对等代码评审](#perform-peer-code-review)

![空复选框](images/checkbox.png)[管理驱动程序访问控制](#manage-driver-access-control)

![空复选框](images/checkbox.png)[增强设备安装安全性](#enhance-device-installation-security)

![空复选框](images/checkbox.png)[执行正确的发布驱动程序签名](#execute-proper-release-driver-signing)

![空复选框](images/checkbox.png)[使用 Visual Studio 中的代码分析来调查驱动程序安全性](#use-code-analysis-in-visual-studio-to-investigate-driver-security)

![空复选框](images/checkbox.png)[使用静态驱动程序验证程序检查是否存在漏洞](#use-static-driver-verifier-to-check-for-vulnerabilities)

![空复选框](images/checkbox.png)[检查带有 BinSkim 二进制分析器的代码](#check-code-with-the-binskim-binary-analyzer)

![空复选框](images/checkbox.png)[使用代码验证工具](#use-additional-code-validation-tools)

![空复选框](images/checkbox.png)[查看调试器技术和扩展](#review-debugger-techniques-and-extensions)

![空复选框](images/checkbox.png)[查看安全编码资源](#review-secure-coding-resources)

[要点总结](#summary-of-key-takeaways)

## <a name="confirm-that-a-kernel-driver-is-required"></a>确认需要内核驱动程序

**安全清单项 \# 1：** *确认内核驱动程序是必需的，并且不能更好地选择较低的风险方法（如 Windows 服务或应用）。*

Windows 内核中的驱动程序在内核中执行时会出现问题。 如果有任何其他选项可用，则与创建新的内核驱动程序相比，它可能会降低成本并降低关联的风险。
有关使用内置 Windows 驱动程序的详细信息，请参阅 [是否需要编写驱动程序？](../gettingstarted/do-you-need-to-write-a-driver-.md)。

有关使用后台任务的信息，请参阅使用  [后台任务支持应用](/windows/uwp/launch-resume/support-your-app-with-background-tasks)。

有关使用 Windows 服务的信息，请参阅 [服务](/windows/desktop/Services/services)。

## <a name="use-the-driver-frameworks"></a>使用驱动程序框架

**安全检查表项 \# 2：** *使用驱动程序框架减小代码大小并提高其可靠性和安全性。*

使用 [Windows 驱动程序框架](../wdf/index.md) 减小代码大小并提高其可靠性和安全性。  若要开始，请查看 [使用 WDF 开发驱动程序](../wdf/using-the-framework-to-develop-a-driver.md)。 有关使用低风险用户模式框架驱动程序 (UMDF) 的信息，请参阅 [选择驱动程序模型](../gettingstarted/choosing-a-driver-model.md)。

[Windows 驱动模型 (WDM) ](../kernel/writing-wdm-drivers.md)驱动程序编写一种旧的方式会更耗费时间和成本，几乎始终都需要重新创建驱动程序框架中提供的代码。

Windows 驱动程序框架源代码是开放源代码，在 GitHub 上可用。 Windows 10 中提供的 WDF 运行时库是根据此源代码生成的。 如果能够按照驱动程序和 WDF 之间的交互步骤进行操作，则可更有效地调试驱动程序。 从下载 [https://github.com/Microsoft/Windows-Driver-Frameworks](https://github.com/Microsoft/Windows-Driver-Frameworks) 。

## <a name="control-access-to-software-only-drivers"></a>控制对仅软件驱动程序的访问

**安全清单项目 \# 3：** *如果要创建仅软件驱动程序，则必须实现其他访问控制。*

仅软件内核驱动程序不使用即插即用 (PnP) 会与特定硬件 Id 相关联，并且可以在任何电脑上运行。 此类驱动程序可用于除最初目的之外的其他用途，从而创建攻击向量。

由于仅软件内核驱动程序包含额外的风险，因此必须将其限制为仅在特定硬件上运行 (例如，通过使用唯一的 PnP ID 启用 PnP 驱动程序的创建，或检查 SMBIOS 表中是否存在特定硬件) 。

例如，假设 OEM Fabrikam 要分发一个驱动程序，该驱动程序为其系统启用超频实用程序。  如果要在不同 OEM 的系统上执行此仅软件驱动程序，则可能会导致系统不稳定或损坏。  Fabrikam 的系统应包含唯一的 PnP ID，以允许创建也可通过 Windows 更新更新的 PnP 驱动程序。  如果这是不可能的，并且 Fabrikam 作者是旧的驱动程序，则该驱动程序应找到另一种方法来验证它是否正在 Fabrikam 系统上执行 (例如，通过在启用任何功能) 之前检查 SMBIOS 表。

## <a name="do-not-production-sign-test-code"></a>不生产签名测试代码

**安全检查表项目 \# 4：** *不生产代码签名开发、测试和制造内核驱动程序代码。*

用于开发、测试或制造的内核驱动程序代码可能包含带来安全风险的危险功能。  此危险代码决不会使用 Windows 信任的证书进行签名。  执行危险驱动程序代码的正确机制是禁用 UEFI 安全启动，启用 BCD "TESTSIGNING"，并使用不受信任的证书对开发、测试和制造代码进行签名 (例如，makecert.exe) 生成的证书。

受信任的软件发行者证书签名的代码 (SPC) 或 Windows 硬件质量实验室 (WHQL) 签名不得便于绕过 Windows 代码完整性和安全技术。  在通过受信任的 SPC 或 WHQL 签名对代码进行签名之前，请先确保它符合 [创建可靠 Kernel-Mode 驱动程序](../kernel/creating-reliable-kernel-mode-drivers.md)的指南。 此外，代码不得包含任何危险行为，如下所述。  有关驱动程序签名的详细信息，请参阅本文后面的 [发布驱动程序签名](#execute-proper-release-driver-signing) 。

危险行为的示例包括：

- 提供将任意内核、物理或设备内存映射到用户模式的功能。
- 提供读取或写入任意内核、物理或设备内存的功能，包括端口输入/输出 (i/o) 。
- 提供跳过 Windows 访问控制的存储的访问权限。
- 用于修改驱动程序设计为不管理的硬件或固件。  

## <a name="perform-threat-analysis"></a>执行威胁分析

**安全检查表项目 \# 5：** *修改现有的驱动程序威胁模型或创建自定义的驱动程序威胁模型。*

考虑到安全性，一种常见的方法是创建具体的威胁模型，以尝试描述可能的攻击类型。 设计驱动程序时，此方法非常有用，因为它会强制开发人员提前考虑潜在的攻击媒介。 如果已确定潜在的威胁，驱动程序开发人员就可以考虑防御这些威胁，从而加强驱动程序组件的总体安全性。

本文提供了有关创建轻型威胁模型的特定于驱动程序的指南： [驱动程序的威胁建模](threat-modeling-for-drivers.md)。 本文提供了一个示例驱动程序威胁模型关系图，可将其用作驱动程序的起点。

![假设内核模式驱动程序的示例数据流图表](images/sampledataflowdiagramkernelmodedriver.gif)

Ihv 和 Oem 可以使用安全开发生命周期 (SDL) 最佳实践和相关工具来提高产品的安全性。 有关详细信息，请参阅 [适用于 oem 的 SDL 建议](../bringup/security-overview.md#sdl-recommendations-for-oems)。

## <a name="follow-driver-secure-coding-guidelines"></a>遵循驱动程序安全编码准则

**安全清单项目 \# 6：** *检查代码并删除任何已知的代码漏洞。*

创建安全驱动程序的核心活动是识别代码中需要更改的区域，以避免已知的软件漏洞。 其中的许多已知软件漏洞都涉及到严格跟踪内存使用情况，以避免他人覆盖或包含驱动程序使用的内存位置的问题。

本文的 [代码验证工具](#use-additional-code-validation-tools) 部分介绍了可用于帮助查找已知软件漏洞的软件工具。

### <a name="memory-buffers"></a>内存缓冲区

- 请始终检查输入缓冲区和输出缓冲区的大小，以确保缓冲区可以容纳所有请求的数据。 有关详细信息，请参阅 [检查缓冲区大小失败](../kernel/failure-to-check-the-size-of-buffers.md)。

- 在将所有输出缓冲区返回给调用方之前，请正确地将其初始化为零。 有关详细信息，请参阅 [初始化输出缓冲区失败](../kernel/failure-to-initialize-output-buffers.md)。

- 验证长度可变的缓冲区。 有关详细信息，请参阅 [验证 Variable-Length 缓冲区失败](../kernel/failure-to-validate-variable-length-buffers.md)。 有关使用缓冲区并使用 [**ProbeForRead**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread) 和 [**ProbeForWrite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite) 验证缓冲区的地址的详细信息，请参阅 [缓冲区处理](../ifs/buffer-handling.md)。

#### <a name="use-the-appropriate-method-for-accessing--data-buffers-with-ioctls"></a>使用适当的方法通过 IOCTLs 访问数据缓冲区

Windows 驱动程序的主要职责之一是在用户模式应用程序和系统设备之间传输数据。 下表显示了用于访问数据缓冲区的三种方法。

| IOCTL 缓冲区类型                     | 总结                          | 更多信息                                                                        |
|---------------------------------------|----------------------------------|---------------------------------------------------------------------------------------------|
| METHOD_BUFFERED                       | 建议用于大多数 situtations | [使用缓冲 I/O](../kernel/using-buffered-i-o.md)                                       |
| METHOD_IN_DIRECT 或 METHOD_OUT_DIRECT | 用于某些高速硬件 i/o   | [使用直接 I/O](../kernel/using-direct-i-o.md)                                           |
| METHOD_NEITHER                        | 尽可能避免                | [既不使用缓冲 I/O，也不使用直接 I/O](../kernel/using-neither-buffered-nor-direct-i-o.md) |

建议使用一般的缓冲 i/o，因为它提供最安全的缓冲方法。 但即使使用缓冲 i/o 也存在风险，如必须缓解的嵌入指针。

有关在 IOCTLs 中使用缓冲区的详细信息，请参阅 [访问数据缓冲区的方法](../kernel/methods-for-accessing-data-buffers.md)。

#### <a name="errors-in-use-of-ioctl-buffered-io"></a>对 IOCTL 缓冲 i/o 使用错误

- 检查 IOCTL 相关缓冲区的大小。 有关详细信息，请参阅 [检查缓冲区大小失败](../kernel/failure-to-check-the-size-of-buffers.md)。

- 正确初始化输出缓冲区。 有关详细信息，请参阅 [初始化输出缓冲区失败](../kernel/failure-to-initialize-output-buffers.md)。

- 正确验证长度可变的缓冲区。 有关详细信息，请参阅 [验证 Variable-Length 缓冲区失败](../kernel/failure-to-validate-variable-length-buffers.md)。

- 使用缓冲 i/o 时，请确保并在 [IO_STATUS_BLOCK](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构信息字段中为 OutputBuffer 返回正确的长度。  不要直接从读取请求直接返回长度。  例如，假设有这样一种情况：用户空间返回的数据指示存在4K 缓冲区。  如果驱动程序实际只应返回200字节，而只是在信息字段中返回4K，则会出现信息泄漏漏洞。 出现此问题的原因在于，在 Windows 的早期版本中，i/o 管理器用于缓冲 i/o 的缓冲区未归零。  这样，用户应用将获取原始200字节的数据，以及缓冲区中的所有数据量为 4K-200 字节 (非分页池内容) 。 这种情况可能发生在所有使用缓冲 i/o 的情况下，而不只是与 IOCTLs 一起使用。

#### <a name="errors-in-ioctl-direct-io"></a>IOCTL 直接 i/o 中的错误

正确处理长度为零的缓冲区。 有关详细信息，请参阅 [直接 i/o 中的错误](../kernel/errors-in-direct-i-o.md)。

#### <a name="errors-in-referencing-user-space-addresses"></a>引用用户空间地址时出错

- 验证嵌入在缓冲 i/o 请求中的指针。 有关详细信息，请参阅 [引用 User-Space 地址中的错误](../kernel/errors-in-referencing-user-space-addresses.md)。

- 在尝试使用用户空间中的任何地址之前，请使用 [**ProbeForRead**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread) 和 [**ProbeForWrite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite) 之类的 api （如果适用）。

#### <a name="toctou-vulnerabilities"></a>TOCTOU 漏洞

使用 IOCTLs 的直接 i/o (或读/写) 时，可能会有 [时间检查使用时间](https://en.wikipedia.org/wiki/Time_of_check_to_time_of_use) (TOCTOU) 漏洞。  请注意，驱动程序正在访问用户数据缓冲区，用户可以同时访问它。

若要管理此风险，请将需要验证的所有参数从用户数据缓冲区复制到仅从内核模式 (的内存，如堆栈或池) 。  然后，用户应用程序无法访问数据后，验证并操作传入的数据。

### <a name="driver-code-must-make-correct-use-of-memory"></a>驱动程序代码必须正确使用内存

- 所有驱动程序池分配都必须位于不可执行的 (NX) 池中。 使用 NX 内存池本质上比使用非分页 (NP) 池的可执行文件更安全，并提供更好的保护来防范溢出攻击。

- 设备驱动程序必须正确处理各种用户模式，以及内核到内核 i/o 和请求。

若要允许驱动程序支持要求 HVCI 虚拟化，需要额外的内存。 有关详细信息，请参阅本文后面的 [要求 hvci 兼容性](#validate-hvci-compatibility) 。

### <a name="handles"></a>句柄数

- 验证在用户模式和内核模式内存之间传递的句柄。 有关详细信息，请参阅 [处理管理](../ifs/handle-management.md) 和 [验证对象句柄失败](../kernel/failure-to-validate-object-handles.md)。

### <a name="device-objects"></a>设备对象

- 保护设备对象。 有关详细信息，请参阅 [保护设备对象](../kernel/controlling-device-access.md)。

- 验证设备对象。 有关详细信息，请参阅 [无法验证设备对象](../kernel/failure-to-validate-device-objects.md)。

### <a name="irps"></a>Irp

#### <a name="wdf-and-irps"></a>WDF 和 Irp

使用 WDF 的一个优点是，WDF 驱动程序通常不会直接访问 Irp。 例如，框架将表示读取、写入和设备 i/o 控制操作的 WDM Irp 转换为在 i/o 队列中 KMDF/UMDF 接收的框架请求对象。

如果要编写 WDM 驱动程序，请查看以下指南。

#### <a name="properly-manage-irp-io-buffers"></a>正确管理 IRP i/o 缓冲区

以下文章提供了有关验证 IRP 输入值的信息：

[使用缓冲 I/O 执行 DispatchReadWrite](../kernel/dispatchreadwrite-using-buffered-i-o.md)

[缓冲 I/O 出错](../kernel/failure-to-check-the-size-of-buffers.md)

[使用直接 I/O 执行 DispatchReadWrite](../kernel/dispatchreadwrite-using-direct-i-o.md)

[直接 I/O 出错](../kernel/errors-in-direct-i-o.md)

[I/O 控制代码的安全问题](../kernel/security-issues-for-i-o-control-codes.md)

请考虑验证与 IRP 关联的值，例如缓冲区地址和长度。

如果你选择不使用 i/o，请注意，与读取和写入不同，与缓冲 i/o 和直接 i/o 不同，在使用 i/o IOCTL 时，i/o 管理器不会验证缓冲区指针和长度。  

#### <a name="handle-irp-completion-operations-properly"></a>正确处理 IRP 完成操作

驱动程序绝不能完成状态值为 "成功" 的 IRP， \_ 除非它实际支持和处理 irp。 有关处理 IRP 完成操作的正确方法的信息，请参阅 [完成 irp](../kernel/completing-irps.md)。

#### <a name="manage-driver-irp-pending-state"></a>管理驱动程序 IRP 挂起状态

驱动程序在保存 IRP 之前应将 IRP 标记为 "挂起"，并且应考虑同时包含对 [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) 的调用和互锁序列中的分配。 有关详细信息，请参阅[在设备暂停时](../kernel/holding-incoming-irps-when-a-device-is-paused.md)[检查驱动程序的状态](../kernel/failure-to-check-a-driver-s-state.md)并保存传入的 irp。

#### <a name="handle-irp-cancellation-operations-properly"></a>正确处理 IRP 取消操作

取消操作很难正确编码，因为它们通常以异步方式执行。 处理取消操作的代码中的问题可能会很长时间被忽略，因为通常不会在运行的系统中频繁执行此代码。 务必阅读并了解 [取消 irp](../kernel/canceling-irps.md)下提供的所有信息。 [在取消 Irp 时，请](../kernel/points-to-consider-when-canceling-irps.md)特别注意[同步 IRP 取消](../kernel/synchronizing-irp-cancellation.md)和要考虑的事项。

最大程度地减少与取消操作关联的同步问题的一种建议方法是实现 [取消安全 IRP 队列](../kernel/cancel-safe-irp-queues.md)。

#### <a name="handle-irp-cleanup-and-close-operations-properly"></a>正确处理 IRP 清理并关闭操作

请确保了解 [**IRP \_ mj \_ 清除**](../kernel/irp-mj-cleanup.md) 和 [**irp \_ mj \_ 关闭**](../kernel/irp-mj-close.md) 请求之间的差异。 清理请求在应用程序关闭文件对象上的所有句柄之后，但有时在所有 i/o 请求完成之前到达。 完成或取消对文件对象的所有 i/o 请求后，关闭请求即可到达。 有关详细信息，请参阅下列文章：

[DispatchCreate、DispatchClose 和 DispatchCreateClose 例程](../kernel/dispatchcreate--dispatchclose--and-dispatchcreateclose-routines.md)

[DispatchCleanup 例程](../kernel/dispatchcleanup-routines.md)

[处理清理和关闭操作时出错](../kernel/errors-in-handling-cleanup-and-close-operations.md)

有关正确处理 Irp 的详细信息，请参阅 [处理 irp 中的其他错误](../kernel/additional-errors-in-handling-irps.md)。

### <a name="other-security-issues"></a>其他安全问题

- 使用锁定或联锁序列来防止争用条件。 有关详细信息，请参阅 [多处理器环境中的错误](../kernel/errors-in-a-multiprocessor-environment.md)。

- 确保设备驱动程序能够正确处理各种用户模式以及内核 i/o 请求。

- 确保在安装或使用过程中，驱动程序或未安装 TDI 筛选器或 Lsp。

#### <a name="use-safe-functions"></a>使用安全函数

- 使用安全字符串函数。 有关详细信息，请参阅 [使用安全字符串函数](../kernel/using-safe-string-functions.md)。

- 使用安全算术函数。 有关详细信息，请参阅[安全整数库例程](/windows-hardware/drivers/ddi/index)中的[算术函数](/windows-hardware/drivers/ddi/index)

- 使用安全转换函数。 有关详细信息，请参阅[安全整数库例程](/windows-hardware/drivers/ddi/index)中的[转换函数](/windows-hardware/drivers/ddi/index)

### <a name="additional-code-vulnerabilities"></a>其他代码漏洞

除了本文所述的可能的漏洞之外，本文还提供了有关增强内核模式驱动程序代码的安全性的其他信息： [创建可靠 Kernel-Mode 驱动程序](../kernel/creating-reliable-kernel-mode-drivers.md)。

有关 C 和 c + + 安全编码的其他信息，请参阅本文末尾的 [安全编码资源](#review-secure-coding-resources) 。

## <a name="manage-driver-access-control"></a>管理驱动程序访问控制

**安全核对清单项 \# 7：** 检查您的 *驱动程序，确保正确控制访问权限。*

### <a name="managing-driver-access-control---wdf"></a>管理驱动程序访问控制-WDF

驱动程序必须工作，以防止用户不正当地访问计算机的设备和文件。 若要防止对设备和文件进行未经授权的访问，你必须：

- 仅在必要时命名设备对象。 命名设备对象通常只是出于传统原因所必需的，例如，如果应用程序需要使用特定的名称打开设备，或者使用非 PNP 设备/控制设备。  请注意，WDF 驱动程序无需命名它们的 PnP 设备 FDO 即可使用 [WdfDeviceCreateSymbolicLink](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatesymboliclink)创建符号链接。

- 安全访问设备对象和接口。

为了使应用程序或其他 WDF 驱动程序能够访问 PnP 设备 PDO，你应该使用设备接口。 有关详细信息，请参阅 [使用设备接口](../wdf/using-device-interfaces.md)。 设备接口用作设备堆栈 PDO 的符号链接。

控制 PDO 访问权限的举世无双方法之一是在 INF 中指定一个 SDDL 字符串。 如果 SDDL 字符串不在 INF 文件中，则 Windows 将应用默认安全描述符。 有关详细信息，请参阅[为设备](../kernel/sddl-for-device-objects.md)对象[保护设备对象](../kernel/controlling-device-access.md)和 SDDL。

有关控制访问的详细信息，请参阅以下文章：

[在 KMDF 驱动程序中控制设备访问权限](../wdf/controlling-device-access-in-kmdf-drivers.md)

[名称、安全描述符和设备类-使设备对象可访问 .。。](https://www.osr.com/nt-insider/2017-issue1/making-device-objects-accessible-safe/) 从 *2017 年1月1日起* ， [OSR](https://www.osr.com)发布的 NT 有问必答新闻稿。

### <a name="managing-driver-access-control---wdm"></a>管理驱动程序访问控制-WDM

如果使用的是 WDM 驱动程序，并且使用的是命名设备对象，则可以使用 [IoCreateDeviceSecure](/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure) 并指定 SDDL 来保护它。 实现 [IoCreateDeviceSecure](/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure) 时，请始终指定 DeviceClassGuid 的自定义类 GUID。 不应在此指定现有的类 GUID。 这样做可能会中断属于该类的其他设备的安全设置或兼容性。 有关详细信息，请参阅 [WdmlibIoCreateDeviceSecure](/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)。

有关详细信息，请参阅下列文章：

[控制设备访问权限](../kernel/controlling-device-access.md)

[控制设备命名空间访问权限](../kernel/controlling-device-namespace-access.md)

[适用于驱动程序开发人员的 Windows 安全模型](windows-security-model.md)

## <a name="security-identifiers-sids-risk-hierarchy"></a>Sid) 风险层次结构 (安全标识符

以下部分介绍了驱动程序代码中使用的常见 Sid 的风险层次结构。 有关 SDDL 的一般信息，请参阅 [sddl 了解设备对象](../kernel/sddl-for-device-objects.md)、 [SID 字符串](/windows/desktop/SecAuthZ/sid-strings)和 [sddl 字符串语法](/openspecs/windows_protocols/ms-dtyp/f4296d69-1c0f-491f-9587-a960b292d070)。

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

### <a name="wdm-granular-ioctl-security-control"></a>WDM 精细 IOCTL 安全控制

为了进一步管理用户模式调用方发送 IOCTLs 时的安全性，驱动程序代码可以包括 [IoValidateDeviceIoControlAccess](/windows-hardware/drivers/ddi/wdm/nf-wdm-iovalidatedeviceiocontrolaccess) 函数。 此函数允许驱动程序检查访问权限。 接收 IOCTL 后，驱动程序可以调用 [IoValidateDeviceIoControlAccess](/windows-hardware/drivers/ddi/wdm/nf-wdm-iovalidatedeviceiocontrolaccess)，同时指定 FILE_READ_ACCESS、FILE_WRITE_ACCESS 或两者。

实现精细的 IOCTL 安全控制不会取代使用上述技术来管理驱动程序访问的需要。

有关详细信息，请参阅下列文章：

[定义 I/O 控制代码](../kernel/defining-i-o-control-codes.md)

## <a name="validate-hvci-compatibility"></a>验证要求 HVCI 兼容性

**安全清单项 \# 8：** *验证驱动程序是否使用了内存，使其与要求 hvci 兼容。*

### <a name="memory-usage-and-hvci-compatibility"></a>内存使用情况和要求 HVCI 的兼容性

要求 HVCI 使用硬件技术和虚拟化将代码完整性与操作系统的其余部分) 决策功能 (隔离开来。 使用基于虚拟化的安全性隔离 CI 时，内核内存可执行的唯一方式是通过 CI 验证。 这意味着内核内存页永远不能为可写的，并且可执行 (W + X) 并且可执行代码不能直接修改。

若要实现要求 HVCI 兼容的代码，请确保你的驱动程序代码执行以下操作：

- 默认情况下，使用 NX
- 使用 NX Api/flags (NonPagedPoolNx) 的内存分配
- 不使用可写和可执行的节
- 不尝试直接修改可执行系统内存
- 不使用内核中的动态代码
- 不将数据文件加载为可执行文件
- 节对齐是 (页面大小) 的0x1000 的倍数 \_ 。 例如 驱动程序 \_ 对齐 = 0x1000

有关使用该工具和不兼容的内存调用列表的详细信息，请参阅 [评估要求 hvci 驱动程序兼容性](use-device-guard-readiness-tool.md)。

有关相关系统基础安全测试的详细信息，请参阅 [设备保护性测试](/windows-hardware/test/hlk/testref/10c242b6-49f6-491d-876c-c39b22b36abc) 和 [与设备保护的驱动程序兼容性](/windows-hardware/test/hlk/testref/driver-compatibility-with-device-guard)。

## <a name="follow-technology-specific-code-best-practices"></a>遵循特定于技术的代码最佳做法

**安全核对清单项 \# 9：** *查看适用于你的驱动程序的以下特定于技术的指南。*

### <a name="file-systems"></a>文件系统

有关详细信息，请参阅以下文章：

[文件系统安全性简介](/windows-hardware/drivers/ifs/introduction-to-file-systems-security)

[文件系统安全问题](../ifs/file-system-security-issues.md)

[文件系统的安全功能](../ifs/security-features-for-file-systems.md)

[与其他文件系统筛选器驱动程序共存](/windows-hardware/drivers/ifs/coexistence-with-other-file-system-filter-drivers)

### <a name="ndis---networking"></a>NDIS-网络

有关 NDIS 驱动程序安全的信息，请参阅 [网络驱动程序的安全问题](../network/security-issues-for-network-drivers.md)。

### <a name="display"></a>显示

有关显示驱动程序安全性的信息，请参阅 &lt; 内容挂起 &gt; 。

### <a name="printers"></a>打印机

有关打印机驱动程序安全的信息，请参阅 [V4 打印机驱动程序安全注意事项](../print/v4-printer-driver-security-considerations.md)。

### <a name="security-issues-for-windows-image-acquisition-wia-drivers"></a>Windows 映像采集 (WIA) 驱动程序的安全问题

有关 WIA 安全性的信息，请参阅 [Windows 图像获取的安全问题 (WIA) 驱动程序](../image/security-issues-for-wia-drivers.md)。

## <a name="enhance-device-installation-security"></a>增强设备安装安全性

**安全清单项 \# 10：** *查看驱动程序 inf 创建和安装指南，以确保遵循最佳做法。*

当你创建用于安装驱动程序的代码时，必须确保始终以安全的方式执行你的设备安装。 安全设备安装是指执行以下操作的设备：

- 限制对设备及其设备接口类的访问
- 限制对为设备创建的驱动程序服务的访问权限
- 保护驱动程序文件不被修改或删除
- 限制对设备的注册表项的访问
- 限制对设备的 WMI 类的访问
- 正确使用 Setupapi.log 函数

有关详细信息，请参阅下列文章：

[创建安全的设备安装](../install/creating-secure-device-installations.md)

[SetupAPI 使用指南](../install/guidelines-for-using-setupapi.md)

[使用设备安装函数](../install/using-device-installation-functions.md)

[设备和驱动程序安装高级主题](../install/creating-secure-device-installations.md)

## <a name="perform-peer-code-review"></a>执行对等代码评审

**安全清单项 \# 11：** *执行对等代码评审，以查找其他工具和进程未*显示的问题

寻找熟悉的代码审阅者，查找可能丢失的问题。 另一组眼睛通常会发现可能已被忽略的问题。

如果你没有适当的员工在内部查看代码，请考虑为此目的提供外部帮助。

## <a name="execute-proper-release-driver-signing"></a>执行正确的发布驱动程序签名

**安全检查表项目 \# 12：** *使用 Windows 合作伙伴门户对驱动程序进行正确的签名以进行分发。*

在公开发布驱动程序包之前，我们建议你先提交程序包以进行认证。 有关详细信息，请参阅对 [性能和兼容性进行测试](/windows-hardware/test/index)， [开始使用硬件计划](../dashboard/get-started-with-the-hardware-dashboard.md)、 [硬件仪表板服务](../dashboard/index.yml)以及使用 [公共发布的内核驱动程序进行签名](../dashboard/attestation-signing-a-kernel-driver-for-public-release.md)。

## <a name="use-code-analysis-in-visual-studio-to-investigate-driver-security"></a>在 Visual Studio 中使用代码分析来调查驱动程序安全性

**安全检查表项目 \# 13：** *按照以下步骤使用 Visual Studio 中的代码分析功能检查驱动程序代码中的漏洞。*

使用 Visual Studio 中的代码分析功能来检查代码中的安全漏洞。 Windows 驱动程序工具包 (WDK) 安装用于检查本机驱动程序代码中的问题的规则集。

有关详细信息，请参阅 [如何对驱动程序运行代码分析](../devtest/how-to-run-code-analysis-for-drivers.md)。

有关详细信息，请参阅 [驱动程序代码分析概述](../devtest/code-analysis-for-drivers-overview.md)。 有关代码分析的更多背景知识，请参阅 [深层 Visual Studio 2013 静态代码分析](/archive/blogs/hkamel/visual-studio-2013-static-code-analysis-in-depth-what-when-and-how)。

若要熟悉代码分析，可以使用示例驱动程序之一（例如，精选的 toaster 示例） <https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster/toastDrv/kmdf/func/featured> 或 ELAM 初期启动的反恶意软件示例 <https://github.com/Microsoft/Windows-driver-samples/tree/master/security/elam> 。

1. 在 Visual Studio 中打开驱动程序解决方案。

2. 在 Visual Studio 中，对于解决方案中的每个项目，将项目属性更改为使用所需的规则集。 例如：项目 &gt; &gt; 属性 &gt; &gt; 代码分析 &gt; &gt; 常规，请选择 "*推荐的驱动程序规则*"。 除了使用 recommenced 驱动程序规则之外，还可以使用 " *建议的本机规则* " 规则集。

3. 选择 &gt; &gt; "生成" "对解决方案运行代码分析"。

4. 在 Visual Studio 中的 "生成输出" 窗口的 " **错误列表** " 选项卡中查看警告。

选择每个警告的说明，以查看代码中有问题的区域。

选择链接的警告代码以查看其他信息。

确定是否需要更改你的代码，或者是否需要添加批注以允许代码分析引擎正确遵循你的代码的意图。 有关代码批注的详细信息，请参阅 [使用 SAL 注释减少 C/c + + 代码缺陷](/visualstudio/code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects) 和 [适用于 Windows 驱动程序的 SAL 2.0 批注](../devtest/sal-2-annotations-for-windows-drivers.md)。

有关 SAL 的一般信息，请参阅 OSR 中的这篇文章。
[https://www.osr.com/blog/2015/02/23/sal-annotations-dont-hate-im-beautiful/](https://www.osr.com/blog/2015/02/23/sal-annotations-dont-hate-im-beautiful/)

## <a name="use-static-driver-verifier-to-check-for-vulnerabilities"></a>使用静态驱动程序验证程序检查是否存在漏洞

**安全检查表项 \# 14：** *按照以下步骤操作，在 Visual Studio 中使用静态驱动程序验证器 (SDV) 检查驱动程序代码中的漏洞。*

静态驱动程序验证器 (SDV) 使用一组接口规则和操作系统模型来确定驱动程序是否与 Windows 操作系统正确交互。 SDV 在驱动程序代码中查找一些缺陷，这些缺陷可能指向驱动程序中的潜在 bug。

有关详细信息，请参阅 [静态驱动程序验证程序](../devtest/introducing-static-driver-verifier.md) 和 [静态驱动程序验证程序](../devtest/static-driver-verifier.md)简介。 

请注意，SDV 仅支持某些类型的驱动程序。 有关 SDV 可以验证的驱动程序的详细信息，请参阅 [支持的驱动程序](../devtest/supported-drivers.md)。 请参阅以下页面，了解有关可用于所使用的驱动程序类型的 SDV 测试的信息。

- [WDM 驱动程序的规则](../devtest/sdv-rules-for-wdm-drivers.md)
- [KMDF 驱动程序的规则](../devtest/sdv-rules-for-kmdf-drivers.md)
- [NDIS 驱动程序的规则](../devtest/sdv-rules-for-ndis-drivers.md)
- [Storport 驱动程序的规则](../devtest/sdv-rules-for-storport-drivers.md)
- [音频驱动程序的规则](../devtest/rules-for-audio-drivers.md)
- [AVStream 驱动程序的规则](../devtest/rules-for-avstream-drivers.md)

若要熟悉 SDV，可以使用一个示例驱动程序 (例如，特色 toaster 示例： " <https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster/toastDrv/kmdf/func/featured>) "。

1. 在 Visual Studio 中打开目标驱动程序解决方案。

2. 在 Visual Studio 中，将生成类型更改为 " *发布*"。 静态驱动程序验证程序要求生成类型为 release，而不是调试。

3. 在 Visual Studio 中，选择 "生成" "生成 &gt; &gt; 解决方案"。

4. 在 Visual Studio 中，选择 "驱动程序 &gt; &gt; 启动静态驱动程序验证程序"。

5. 在 SDV 的 "*规则*" 选项卡上，选择 "*规则集*" 下的 "*默认*"。

   尽管默认规则发现许多常见问题，但也请考虑运行更全面的 " *所有驱动程序规则* " 规则集。

6. 在 SDV 的 *主* 选项卡上，选择 " *启动*"。

7. 当 SDV 完成时，查看输出中的任何警告。 *主*选项卡显示发现的缺陷总数。

8. 选择每个警告以加载 "SDV 报表" 页，并检查与可能的代码漏洞关联的信息。 使用报表调查验证结果，并确定驱动程序中 SDV 验证失败的路径。 有关详细信息，请参阅 [静态驱动程序验证程序报表](../devtest/static-driver-verifier-report.md)。

## <a name="check-code-with-the-binskim-binary-analyzer"></a>用 BinSkim 二进制分析器检查代码

**安全核对清单项 \# 15：** *按照以下步骤进行操作，以使用 BinSkim 来仔细检查是否配置了编译和生成选项，以最大程度地减少已知的安全问题。*

使用 BinSkim 来检查二进制文件，以确定编码和构建可能会导致二进制漏洞发生的行为。

BinSkim 检查以下内容：

- 使用过时的编译器工具集-应尽可能使用最新的编译器工具集编译二进制文件，以最大限度地利用当前编译器级别和操作系统提供的安全缓解措施。
- 不安全的编译设置-应使用最安全的设置来编译二进制文件，以启用操作系统提供的安全缓解功能，最大限度地提高编译器错误和可操作的警告报告。
- 签名问题-已签名的二进制文件应该用加密型强算法进行签名。

BinSkim 是一个开源工具，它会生成使用静态分析结果交换格式 ([SARIF](https://github.com/oasis-tcs/sarif-spec)) 格式的输出文件。 BinSkim 替换了以前的 [BinScope](https://www.microsoft.com/security/blog/2014/11/20/new-binscope-released/) 工具。

有关 BinSkim 的详细信息，请参阅 [BinSkim 用户指南](https://github.com/microsoft/binskim/blob/master/docs/UserGuide.md)。

按照以下步骤验证是否已在您要发送的代码中正确配置了安全编译选项。

1. 下载并安装跨平台 [.NET Core SDK](https://dotnet.microsoft.com/download)。

2. 下载 BinSkim 的方法有很多，例如 NuGet 包。 在此示例中，我们将从此处下载包含 BinSkim 的 zip 文件： <https://github.com/microsoft/binskim> 并将其安装在64位 WINDOWS 电脑上。

3. 选择上的 " **克隆或下载** " 按钮 <https://github.com/microsoft/binskim> ，然后选择 " **下载 Zip**"。

4. 选择已下载的 zip 文件并将其解压缩，例如 `C:\binskim-master` 。

5. 确认已安装 Visual Studio。 有关下载和安装 Visual Studio 的信息，请参阅 [安装 Visual studio](/visualstudio/install/install-visual-studio)。

6. 打开 "Visual Studio 开发人员命令提示" 窗口，并移到你将文件解压缩到的目录。  

   ```console
   C:\> Cd \binskim-master
   ```

7. 在登记的根目录下运行 **BuildAndTest** ，以确保发布生成成功，并且所有测试都通过。

   ```console
   C:\binskim-master> BuildAndTest.cmd

   Welcome to .NET Core 3.1!
   ---------------------
   SDK Version: 3.1.101

   ...

   C:\binskim-master\bld\bin\AnyCPU_Release\Publish\netcoreapp2.0\win-x64\BinSkim.Sdk.dll
   1 File(s) copied
   C:\binskim-master\bld\bin\AnyCPU_Release\Publish\netcoreapp2.0\linux-x64\BinSkim.Sdk.dll
   1 File(s) copied

   ...

   ```

8. 生成过程将创建包含 BinSkim 可执行文件的目录集。 转到 win-x64 位生成输出目录。  

   ```console
   C:\binskim-master> Cd \binskim-master\bld\bin\AnyCPU_Release\Publish\netcoreapp2.0\win-x64>
   ```

9. 显示 "分析" 选项的帮助。

   ```console
   C:\binskim-master\bld\bin\AnyCPU_Release\Publish\netcoreapp2.0\win-x64> BinSkim help analyze

   BinSkim PE/MSIL Analysis Driver 1.6.0.0

   --sympath                      Symbols path value, e.g., SRV*http://msdl.microsoft.com/download/symbols or Cache*d:\symbols;Srv*http://symweb. See
                                 https://docs.microsoft.com/windows-hardware/drivers/debugger/advanced-symsrv-use for syntax information. Note that BinSkim will clear the
                                 _NT_SYMBOL_PATH environment variable at runtime. Use this argument for symbol information instead.

   --local-symbol-directories     A set of semicolon-delimited local directory paths that will be examined when attempting to locate PDBs.

   -o, --output                   File path to which analysis output will be written.

   --verbose                      Emit verbose output. The resulting comprehensive report is designed to provide appropriate evidence for compliance scenarios.

   ...
  
   ```

### <a name="setting-the-symbol-path"></a>设置符号路径

如果要在运行 BinSkim 的计算机上生成所有正在分析的代码，则通常不需要设置符号路径。 这是因为符号文件在你编译的本地框中可用。 如果你使用的是更复杂的生成系统，或者将符号重定向到不同的位置 (不与已编译的二进制文件) ，请使用 `--local-symbol-directories` 将这些位置添加到符号文件搜索。
如果代码引用了不是代码一部分的已编译的二进制文件，则可以使用 Window 调试器 sympath 来检索符号，以便验证这些代码依赖项的安全性。 如果在这些依赖关系中发现问题，可能无法修复它们。 但是，若要了解任何可能存在的安全风险，请考虑使用这些依赖项。

> [!TIP]
>添加引用网络符号服务器的符号路径 (时) ，请添加本地缓存位置以指定要缓存符号的本地路径。 不这样做会极大地影响 BinSkim 的性能。 下面的示例在 d:\symbols. 中指定一个本地缓存。
`--sympath Cache*d:\symbols;Srv*http://symweb`
有关 sympath 的详细信息，请参阅 [Windows 调试器的符号路径](../debugger/symbol-path.md)。

1. 执行以下命令来分析已编译的驱动程序二进制文件。 将目标路径更新为指向编译的驱动程序 sys.databases 文件。

   ```console
   C:\binskim-master\bld\bin\AnyCPU_Release\Publish\netcoreapp2.0\win-x64> BinSkim analyze "C:\Samples\KMDF_Echo_Driver\echo.sys"
   ```

2. 有关其他信息，请添加如下的详细选项。

   ```console
   C:\binskim-master\bld\bin\AnyCPU_Release\Publish\netcoreapp2.0\win-x64> BinSkim analyze "C:\Samples\KMDF_Echo_Driver\osrusbfx2.sys" --verbose
   ```

   > [!NOTE]
   >--Verbose 选项将为每个检查产生显式通过/失败结果。 如果未提供详细的，则只会看到 BinSkim 检测到的缺陷。 由于日志文件的大小增加，通常不建议使用--verbose 选项，因为这会使日志文件的大小增加，因此，在发生多个 "pass" 结果时，可能更难选取单个失败。

3. 查看命令输出以查找可能存在的问题。 此示例输出显示了三个通过的测试。 [BinSkim 用户指南](https://github.com/microsoft/binskim/blob/master/docs/UserGuide.md)中提供了有关这些规则的其他信息，例如 BA2002。

   ```console
   Analyzing...
   Analyzing 'osrusbfx2.sys'...
   ...

   C:\Samples\KMDF_Echo_Driver\osrusbfx2.sys\Debug\osrusbfx2.sys: pass BA2002: 'osrusbfx2.sys' does not incorporate any known vulnerable dependencies, as configured by current policy.
   C:\Samples\KMDF_Echo_Driver\Debug\osrusbfx2.sys: pass BA2005: 'osrusbfx2.sys' is not known to be an obsolete binary that is vulnerable to one or more security problems.
   C:\Samples\KMDF_Echo_Driver\osrusbfx2.sys: pass BA2006: All linked modules of 'osrusbfx2.sys' generated by the Microsoft front-end satisfy configured policy (compiler minimum version 17.0.65501.17013).
   ```

4. 此输出显示测试 BA3001 不会运行，因为该工具指示该驱动程序不是 ELF 二进制文件。

   ```console
   ...
   C:\Samples\KMDF_Echo_Driver\Debug\osrusbfx2.sys: notapplicable BA3001: 'osrusbfx2.sys' was not evaluated for check 'EnablePositionIndependentExecutable' as the analysis is not relevant based on observed metadata: image is not an ELF binary.
   ```

5. 此输出显示测试 BA2007 的错误。

   ```console
   ...

   C:\Samples\KMDF_Echo_Driver\Debug\osrusbfx2.sys: error BA2007: 'osrusbfx2.sys' disables compiler warning(s) which are required by policy.
   A compiler warning is typically required if it has a high likelihood of flagging memory corruption, information disclosure, or double-free vulnerabilities.
   To resolve this issue, enable the indicated warning(s) by removing /Wxxxx switches (where xxxx is a warning id indicated here) from your command line, and resolve any warnings subsequently raised during compilation.
   ```

若要在 Visual Studio 中启用这些警告，请在项目的属性页中的 "C/c + +" 下，在 " **禁用特定警告**" 中删除不希望排除的值。

![用于在 Visual Studio 2019 中禁用特定警告的对话框](images/disable-specific-warnings-dialog.png)

Visual Studio 中用于驱动程序项目的默认编译选项可以禁用如下所示的警告。 BinSkim 将报告这些警告。

[C4603-"name"：未定义宏或在预编译标头使用后定义不同](/cpp/error-messages/compiler-warnings/compiler-warning-level-1-c4603)

[C4627-"description"：在查找预编译标头使用时跳过](/cpp/error-messages/compiler-warnings/compiler-warning-level-1-c4627)

[C4986-"声明"：异常规范与前面的声明不匹配](/cpp/error-messages/compiler-warnings/compiler-warning-c4986)

有关编译器警告的详细信息，请参阅编译器 [警告（按编译器版本](/cpp/error-messages/compiler-warnings/compiler-warnings-by-compiler-version)）。

## <a name="use-additional-code-validation-tools"></a>使用其他代码验证工具

**安全核对清单项 \# 16：** *使用这些附加工具来帮助验证你的代码是否遵循安全建议，并探测你的开发过程中丢失的空白。*

除了上面所述 [Visual Studio Code 分析](#use-code-analysis-in-visual-studio-to-investigate-driver-security)、 [静态驱动程序验证程序](#use-static-driver-verifier-to-check-for-vulnerabilities)和 [Binskim](#check-code-with-the-binskim-binary-analyzer) ，还可以使用以下工具来探测开发过程中丢失的缺口。

### <a name="driver-verifier"></a>驱动程序验证程序

驱动程序验证程序允许对驱动程序进行实时测试。 驱动程序验证程序监视 Windows 内核模式驱动程序和图形驱动程序，目的是检测可能损坏系统的非法函数调用或操作。 驱动程序验证程序可将 Windows 驱动程序用于各种强调和测试，以找出不正确的行为。 有关详细信息，请参阅[驱动程序验证程序](../devtest/driver-verifier.md)。

### <a name="hardware-compatibility-program-tests"></a>硬件兼容性计划测试

硬件兼容性程序包含安全相关的测试，可用于查找代码漏洞。 Windows 硬件兼容性计划利用 Windows 硬件实验室工具包中的测试 (HLK) 。 可以在命令行上使用 HLK 设备基础测试来运用驱动程序代码和探测漏洞。 有关设备基础测试和硬件兼容性计划的一般信息，请参阅 [Windows 硬件实验室工具包](/windows-hardware/test/hlk/)。

以下测试是检查与代码漏洞相关的某些行为的驱动程序代码可能很有用的测试示例：

 [DF - 模糊随机 IOCTL 测试（可靠性）](/windows-hardware/test/hlk/testref/236b8ad5-0ba1-4075-80a6-ae9dafb71c94)

 [DF - 模糊 sub-open 测试（可靠性）](/windows-hardware/test/hlk/testref/92bf534e-aa48-4aeb-b3cd-e46fb7cc7d80)

 [DF - 模糊零长度缓冲区 FSCTL 测试（可靠性）](/windows-hardware/test/hlk/testref/5f5f6c7e-d5db-4ff1-8cee-da47203ab070)

 [DF - 模糊随机 FSCTL 测试（可靠性）](/windows-hardware/test/hlk/testref/e529e34e-076a-4978-926f-7eca333e8f4d)

 [DF - 模糊杂项 API 测试（可靠性）](/windows-hardware/test/hlk/testref/fb305d04-6e8c-4dfc-9984-9692df82fbd8)

 你还可以使用驱动程序验证程序附带的 [内核同步延迟模糊](../devtest/kernel-synchronization-delay-fuzzing.md) 处理。

 (并发硬件和操作系统的混乱) 测试会同时运行各种 PnP 驱动程序测试、设备驱动程序模糊测试和电源系统测试。 有关详细信息，请参阅 [ (设备基础) 的混乱测试 ](../devtest/chaos-tests--device-fundamentals-.md)。

设备基础的渗透测试执行各种形式的输入攻击，这是安全测试的关键组成部分。 攻击和渗透测试可帮助识别软件接口中的漏洞。 有关详细信息，请参阅 [渗透测试 (设备基础) ](../devtest/penetration-tests--device-fundamentals-.md)。

使用 [Device Guard 合规性测试](/windows-hardware/test/hlk/testref/10c242b6-49f6-491d-876c-c39b22b36abc)以及本文中所述的其他工具，以确认你的驱动程序与要求 hvci 兼容。

### <a name="custom-and-domain-specific-test-tools"></a>自定义和域特定的测试工具

考虑开发自定义域特定的安全测试。 若要开发其他测试，请从该软件的原始设计器中收集输入，以及熟悉正在开发的特定驱动程序类型的无关开发资源，以及一个或多个熟悉安全入侵分析和防护的人。

## <a name="review-debugger-techniques-and-extensions"></a>查看调试器技术和扩展

**安全清单项目 \# 17：** *查看这些调试器工具并考虑它们在开发调试工作流中的使用。*

### <a name="exploitable-crash-analyzer"></a>！可利用故障分析器

！可利用的故障分析器是一种 Windows 调试程序扩展，用于分析查找独特问题的崩溃日志。 它还检查崩溃类型，并尝试确定错误是否是恶意黑客可以利用的问题。

Microsoft 安全工程中心 (MSEC) ，创建了！可利用的故障分析器。 可以从 codeplex 下载： <https://msecdbg.codeplex.com/> 。

有关详细信息，请参阅 [！可利用的崩溃分析器版本 1.6](https://www.microsoft.com/security/blog/2013/06/13/exploitable-crash-analyzer-version-1-6/) 和第9频道视频 [！可利用故障分析器](https://channel9.msdn.com/blogs/pdcnews/bang-exploitable-security-analyzer)。

### <a name="security-related-debugger-commands"></a>与安全性相关的调试器命令

！ Acl 扩展格式并显示访问控制列表 (ACL) 的内容。 有关详细信息，请参阅 [确定对象的 ACL](../debugger/determining-the-acl-of-an-object.md) 和 [**！ acl**](../debugger/-acl.md)。

！令牌扩展显示安全令牌对象的格式化视图。 有关详细信息，请参阅 [**！ token**](../debugger/-token.md)。

！ Tokenfields 扩展显示 (令牌结构) 的访问令牌对象中的字段的名称和偏移量。 有关详细信息，请参阅 [**！ tokenfields**](../debugger/-tokenfields.md)。

！ Sid 扩展显示指定地址 (SID) 安全标识符。 有关详细信息，请参阅 [**！ sid**](../debugger/-sid.md)。

！ Sd extension 显示指定地址处的安全描述符。 有关详细信息，请参阅 [**！ sd**](../debugger/-sd.md)。

## <a name="review-secure-coding-resources"></a>查看安全编码资源

**安全清单项目 \# 18：** *查看这些资源，以扩展对驱动程序开发人员适用的安全编码最佳实践的了解。*

### <a name="review-these-resources-to-learn-more-about-driver-security"></a>查看这些资源，了解有关驱动程序安全性的详细信息

#### <a name="secure-kernel-mode-driver-coding-guidelines"></a>保护内核模式驱动程序编码准则

[创建可靠的内核模式驱动程序](../kernel/creating-reliable-kernel-mode-drivers.md)

#### <a name="secure-coding-organizations"></a>安全编码组织

[Carnegie 卡内基梅隆大学 SEI 证书](https://www.sei.cmu.edu/about/divisions/cert/index.cfm)

Carnegie 卡内基梅隆大学 SEI CERT [C 编码标准：用于开发安全、可靠和安全系统](https://www.securecoding.cert.org/confluence/display/c/SEI+CERT+C+Coding+Standard) (2016 版) 的规则。

CERT- [生成安全性](https://www.us-cert.gov/bsi)

MITRE- [由 CERT C 安全编码标准解决的漏洞](https://cwe.mitre.org/data/definitions/734.html)

在成熟度模型中构建安全性 (BSIMM) - [https://www.bsimm.com/](https://www.bsimm.com/)

SAFECode - [https://safecode.org/](https://safecode.org/)

#### <a name="osr"></a>OSR

[OSR](https://www.osr.com) 提供驱动程序开发培训和咨询服务。 OSR 新闻稿中的这些文章突出显示了驱动程序安全问题。

[名称、安全描述符和设备类-使设备对象可访问 .。。和安全](https://www.osr.com/nt-insider/2017-issue1/making-device-objects-accessible-safe/)

[已走使用保护--内部驱动程序 & 设备安全](https://www.osronline.com/article.cfm^article=100.htm)

[锁定驱动程序-技术调查](https://www.osronline.com/article.cfm^article=357.htm)

[Meltdown 和 Spectre：驱动程序？](https://www.osr.com/blog/2018/01/23/meltdown-spectre-drivers/)

#### <a name="case-study"></a>案例研究

[从警报到驱动程序漏洞： Microsoft Defender ATP 调查 unearths 特权升级缺陷](https://www.microsoft.com/security/blog/2019/03/25/from-alert-to-driver-vulnerability-microsoft-defender-atp-investigation-unearths-privilege-escalation-flaw/)

#### <a name="books"></a>书籍

*24 抱问题软件安全：* Michael Howard、David LeBlanc 和 John Viega 的编程缺陷和解决方法

*软件安全评估的内容：识别和预防软件漏洞*，将 Dowd、John 麦克唐纳和 Justin Schuh

*编写安全软件 Second Edition*、Michael Howard 和 David LeBlanc

*软件安全评估的内容：识别并防止软件漏洞*，将 Dowd 和约翰麦克唐纳

*C 和 c + + 中的安全编码 (软件工程中的 SEI 系列) 第2版*，Robert Seacord

* (第2版) *，Walter Oney Windows 驱动模型

*开发包含 Windows Driver Foundation (开发人员参考) 、Orwick 和人员 Smith 的驱动程序*

#### <a name="training"></a>培训

可从以下供应商获取 Windows 驱动程序课堂培训：

- [OSR](https://www.osr.com)
- [Winsider](https://www.windows-internals.com/)
- [Azius](https://azius.com/)

可从各种源获取安全编码在线培训。 例如，可以从 coursera 获取此课程：

[https://www.coursera.org/learn/software-security](https://www.coursera.org/learn/software-security).

SAFECode 还提供免费的培训：

[SAFECode.org/training](https://safecode.org/training/)

#### <a name="professional-certification"></a>专业认证

 CERT 提供 [安全的编码专业证书](https://www.sei.cmu.edu/education-outreach/credentials/index.cfm)。

## <a name="summary-of-key-takeaways"></a>要点总结

驱动程序安全性是包含许多元素的复杂任务，但以下是一些需要考虑的要点：

- Windows 内核中的驱动程序在内核中执行时会出现问题。 因此，请密切注意驱动程序安全性和设计，并考虑安全性。

- 应用最小特权原则：

    a. 使用 strict SDDL 字符串限制对驱动程序的访问

    b. 进一步限制单个 IOCTL 的

- 创建威胁模型来识别攻击向量，并考虑是否可以进一步限制任何内容。
- 请注意从 usermode 传入的嵌入式指针。 需要在除之外的 "try" 中对其进行探测、访问，并且在 (ToCToU) 问题的情况下，它们容易出现检查时间使用时间，除非捕获和比较缓冲区的值。
- 如果不确定，请使用 METHOD_BUFFERED 作为 IOCTL 缓冲方法。
- 使用代码扫描实用程序查找已知的代码漏洞并修正任何确定的问题。
- 寻找熟悉的代码审阅者，查找可能丢失的问题。
- 使用驱动程序验证程序并使用多个输入（包括拐角情况）测试驱动程序。
---
title: 验证工具调查
description: 验证工具调查
ms.assetid: d36e041f-efa5-450f-b4de-c84c4880e44d
keywords:
- 动态验证工具 WDK
- 静态验证工具 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 187eaaef53bc8030b91e19142f5db4ce79d52b16
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360934"
---
# <a name="survey-of-verification-tools"></a>验证工具调查


使用以下验证工具是在 WDK 中所述，建议使用驱动程序开发人员和测试人员。 它们在其中，通常会使用顺序列出。

### <a name="span-idassoonasthecodecompilesspanspan-idassoonasthecodecompilesspanas-soon-as-the-code-compiles"></a><span id="as_soon_as_the_code_compiles"></span><span id="AS_SOON_AS_THE_CODE_COMPILES"></span>只要能够编译代码

-   [代码分析驱动程序](code-analysis-for-drivers.md)是运行在编译时静态验证工具。 Windows 驱动程序工具包提供的特定于驱动程序的扩展[代码分析工具](https://go.microsoft.com/fwlink/p/?linkid=226836)Microsoft Visual Studio Ultimate 2012 中。

    [代码分析驱动程序](code-analysis-for-drivers.md)可以验证驱动程序以 C 编写 /C++和托管代码。 它将检查驱动程序的每个函数中的代码独立，以便您可以构建您的驱动程序时，就立即可以运行它。 它运行相对较快，并使用一些资源。

    基本功能[代码分析工具](https://go.microsoft.com/fwlink/p/?linkid=226836)检测常规编码错误，例如不检查返回值。 特定于驱动程序的功能检测更微妙的驱动程序编码错误，如保持未初始化的字段中复制的 IRP 和未能还原更改的 IRQL 例程的结束。

<!-- -->

-   [Static Driver Verifier](static-driver-verifier.md) (SDV) 是一个静态验证工具，在编译时运行，并验证用 C 编写的内核模式驱动程序代码 /C++。 它包含在 WDK 中并从 Visual Studio Ultimate 2012 或 Visual Studio 命令提示窗口中使用 MSBuild 可以启动。

    根据一组接口规则和操作系统的模型，Static Driver Verifier 确定驱动程序是否正确交互与 Windows 操作系统内核。 Static Driver Verifier 是极其全面--它探讨了驱动程序源代码中的所有可访问路径并执行这些符号。 在这种情况下，它会查找使用驱动程序测试的任何其他传统方法来检测不到的 bug。

### <a name="span-idwhenthedriverrunsspanspan-idwhenthedriverrunsspanwhen-the-driver-runs"></a><span id="when_the_driver_runs"></span><span id="WHEN_THE_DRIVER_RUNS"></span>该驱动程序的运行时

使用以下动态验证工具，只要该驱动程序生成和运行时不明显的错误。

-   [已检验版本的 Windows](checked-build-of-windows.md)。 虽然不从技术上讲一个验证工具的 Windows 内部版本上运行您的驱动程序将帮助您检测在使用其他工具进行测试中不可见的错误。 通过将已检验版本与内核调试程序结合来运行，应该是开发和测试驱动程序的一个标准部分。

-   [驱动程序验证程序](driver-verifier.md)是专门为 Windows 驱动程序编写的动态验证工具。 它包括可以同时在多个驱动程序运行的多个测试。 Driver Verifier 是因此高效地查找驱动程序中的驱动程序开发人员遇到严重的 bug 和测试人员配置驱动程序验证程序时其驱动程序运行在开发或测试环境中运行。 驱动程序验证程序包含在 Windows 2000 和更高版本的 Windows。 启用时驱动程序验证程序的驱动程序，也必须驱动程序上运行多个测试。 驱动程序验证工具可以检测某些很难检测到使用静态验证工具单独的驱动程序错误。 这些类型的错误的示例包括：
    -   **内核池的缓冲区溢出。** 当已验证的驱动程序分配池内存缓冲区时，驱动程序验证程序可防止它们与非可访问的内存页。 如果该驱动程序尝试使用的内存超出缓冲区末尾时，驱动程序验证程序将发出的 bug 检查。
    -   **释放后使用的内存。** 特殊的池的内存块使用他们自己的内存页，并不与其他分配共享内存页。 驱动程序正在释放的池内存块，相应的内存页将变为不可访问。 如果驱动程序将尝试使用该内存释放后，该驱动程序将立即崩溃。
    -   **使用提升的 IRQL 在运行时可分页内存。** 当已验证的驱动程序将引发在调度 IRQL\_级别或更高版本，驱动程序验证程序修剪系统工作集，从所有可分页内存模拟内存不足的情况下系统。 如果尝试使用其中一个可分页虚拟地址，该驱动程序崩溃。
    -   **低资源模拟。** 若要模拟的系统资源不足的情况下，驱动程序验证程序可能会失败由驱动程序调用 Api 的各种操作系统内核。
    -   **内存泄漏。** 驱动程序验证程序跟踪所做的驱动程序的内存分配的并确保该驱动程序被卸载之前, 释放内存。
    -   **需要很长时间以完成或取消的 I/O 操作。** 驱动程序验证程序可以测试用于响应状态的驱动程序的逻辑\_PENDING 返回值从[ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)。
    -   **DDI 符合性检查。** （可从 Windows 8 开始）驱动程序验证器应用一组检查驱动程序和操作系统的内核接口之间的正确交互的设备驱动程序接口 (DDI) 规则。 这些规则对应于在分析驱动程序源代码中使用 Static Driver Verifier 的规则。 如果驱动程序验证工具发现错误时启用 DDI 符合性检查，运行[Static Driver Verifier](static-driver-verifier.md)和选择的相同规则，导致该错误。 Static Driver Verifier 可帮助您的驱动程序源代码中找到缺陷的原因。
-   [应用程序验证工具](application-verifier.md)是一个用于用户模式应用程序和驱动程序以 C 编写的动态验证工具 /C++。 它不会验证托管的代码。 应用程序验证程序不包含在 WDK 中，但可以下载并安装它从[Microsoft Download Center](https://go.microsoft.com/fwlink/p/?linkid=11573)。

 

 






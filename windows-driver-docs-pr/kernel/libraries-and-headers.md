---
title: 库和标头
description: 库和标头
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 49703050fa3abd35957db3c0edb0022a9c8465af
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801655"
---
# <a name="libraries-and-headers"></a>库和标头


内核模式驱动程序使用本机系统服务例程，方法是调用 Ntoskrnl.exe 动态链接库中的 **Nt** 和 **Zw** 入口点 (DLL) 。 此 DLL 包含这些例程的实际实现。 为了访问这些入口点，驱动程序将静态链接到 Ntoskrnl.exe 库，该库在 Windows 驱动程序工具包 (WDK) 中可用。 在 Ntoskrnl.exe 中实现的例程是一个存根，它在运行时动态链接到 Ntoskrnl.exe 中的入口点。

WDK 文档介绍 Ntoskrnl.exe 中的某些（但不是全部） **Zw** 入口点。 有关可由驱动程序调用的 **Zw** 例程的说明，请参阅 [ZwXxx 例程](/previous-versions/windows/hardware/drivers/ff567122(v=vs.85))。

大多数记录的 **Zw** 例程在 WDK 的 Wdm 标头文件中定义，但在其他头文件（例如 Ntddk 和 Ntifs）中定义了少数。

通常，用户模式应用程序不调用 **Nt** 和 **Zw** 例程。 相反，应用程序可以调用 Win32 例程，如 [CreateFile](/windows/win32/api/fileapi/nf-fileapi-createfilea)，后者随后调用本机系统服务例程（如 [NtCreateFile](/windows/win32/api/winternl/nf-winternl-ntcreatefile) 或 [**ZwCreateFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)）来执行请求的操作。 但是，用户模式应用程序可能会直接调用 **Nt** 或 **Zw** 例程来执行 Win32 例程不支持的操作。

用户模式应用程序通过调用 Ntdll.dll 动态链接库中的入口点来使用本机系统服务例程。 这些入口点将对 **Nt** 和 **Zw** 例程的调用转换为捕获到内核模式的系统调用。 若要访问这些入口点，用户模式应用程序静态链接到 Ntdll.dll 库（在 WDK 中提供）。 在 Ntdll.dll 中实现的例程是一个存根，它在运行时动态链接到 Ntdll.dll 中的入口点。

Windows SDK 文档介绍了 Ntdll.dll 中的某些（但不是全部） **Nt** 入口点。 大多数记录的 **Nt** 例程是在 Windows SDK 的 Winternl 头文件中定义的。 此文档几乎不会提及 **Zw** 入口点，并且 Windows SDK 包含 **Zw** 例程的定义。

除了几个次要例外外， **Nt** 例程的 Ntdll.dll 中的每个入口点都有一个匹配的 **Zw** 例程入口点。 WDK 和 Windows SDK 的文档建议应用程序开发人员避免调用未记录的 **Nt** 入口点，并警告 **Zw** 入口点可能会 Ntdll.dll 从 Windows 的未来版本中消失。 应为此事件准备从用户模式调用 **Zw** 例程的应用程序开发人员。

有关应用程序可以调用的 **Nt** 例程的说明，请参阅 [Winternl](https://go.microsoft.com/fwlink/p/?linkid=157253)、 [Files](https://go.microsoft.com/fwlink/p/?linkid=157254)和 [其他 Low-Level 客户端支持](/windows/win32/devnotes/-win32-misclowlevelclientsupport)。 Windows SDK 文档中的一些 **Nt** 例程的参考页会将例程标记为 "已弃用"，并建议读者使用等效的 Win32 例程，而不是已弃用的 **Nt** 例程。

用户模式应用程序无法调用 Ntoskrnl.exe 中的入口点，并且内核模式驱动程序无法调用 Ntdll.dll 中的入口点。


---
title: 库和标头
description: 库和标头
ms.assetid: 0d4d0273-775f-4cbb-8b7f-63b22f3ccdae
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 849e879833c40eb06ac63562bbbae10185dd0ae0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381373"
---
# <a name="libraries-and-headers"></a>库和标头


内核模式驱动程序通过调用来使用本机系统服务例程**Nt**并**Zw** Ntoskrnl.exe 动态链接库 (DLL) 中的入口点。 此 DLL 包含这些例程的实际实现。 若要访问这些入口点，驱动程序静态链接到 Ntoskrnl.lib 库，后者是 Windows Driver Kit (WDK) 中可用。 在 Ntoskrnl.lib 中实现的例程是在运行时动态链接到 Ntoskrnl.exe 中的入口点的存根。

WDK 文档介绍了一些，但不是全部**Zw** Ntoskrnl.exe 中的入口点。 有关的说明**Zw**例程可以调用的驱动程序，请参阅[ZwXxx 例程](https://msdn.microsoft.com/library/windows/hardware/ff567122)。

大部分已编档**Zw**例程在 WDK 中 wdm.h 中标头文件中定义，但一些其他标头文件，如 Ntddk.h 和 Ntifs.h 中定义。

通常情况下，用户模式应用程序不调用**Nt**并**Zw**例程。 相反，应用程序可能调用一个 Win32 例程，如[CreateFile](https://go.microsoft.com/fwlink/p/?linkid=152795)，后者随后调用本机系统服务例程，如[NtCreateFile](https://go.microsoft.com/fwlink/p/?linkid=157250)或[ **zwcreatefile 转换** ](https://msdn.microsoft.com/library/windows/hardware/ff566424)，若要执行所请求的操作。 但是，在用户模式应用程序可能直接调用**Nt**或**Zw**例程，以执行 Win32 例程不支持的操作。

用户模式应用程序使用本机系统服务例程通过调用 Ntdll.dll 动态链接库中的入口点。 这些入口点将调用转换为**Nt**并**Zw**执行捕获到内核模式的系统调用的例程。 若要访问这些入口点，在用户模式应用程序静态链接到 Ntdll.lib 库，可在 WDK 中。 在 Ntdll.lib 中实现的例程是在运行时动态链接到 Ntdll.dll 的入口点的存根。

Windows SDK 文档介绍了一些，但不是全部**Nt** Ntdll.lib 中的入口点。 大部分已编档**Nt**例程 Windows SDK 中 Winternl.h 标头文件中定义。 本文档提到小**Zw**入口点和 Windows SDK 中没有标头文件，包含的定义**Zw**例程。

除了几个细微区别，每个入口点中的 Ntdll.dll **Nt**例程具有匹配的入口点**Zw**例程。 WDK 和 Windows SDK 的文档建议应用程序开发人员避免调用未记录**Nt**入口点，并发出的警告**Zw**入口点可能会从 Ntdll.dll 中消失Windows 的未来版本。 应用程序开发人员调用**Zw**从用户模式下的例程应出现这种情况做好准备。

有关的说明**Nt**例程可以调用的应用程序，请参阅[Winternl](https://go.microsoft.com/fwlink/p/?linkid=157253)，[文件](https://go.microsoft.com/fwlink/p/?linkid=157254)，和[其他低级别客户端支持](https://go.microsoft.com/fwlink/p/?linkid=157255). 某些引用了页**Nt**例程 Windows SDK 文档中的标记为"已弃用"例程也建议读者使用而不是不推荐使用的等效 Win32 例程**Nt**例程。

在用户模式应用程序不能在 Ntoskrnl.exe，调用的入口点和内核模式驱动程序不能在 Ntdll.dll 中调用的入口点。

 

 





---
title: 选择 32 位或 64 位调试工具
description: 安装的 Windows 调试工具，可以获取两个 32 位套工具和 64 位一系列工具。
ms.assetid: 26aaaf11-1005-4ae7-8f27-4ae0812faa81
keywords:
- 32 位调试器包
- 32 位调试工具
- 64 位调试器包
- 64 位调试工具
- 安装中，选择 32 位和 64 位包之间
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03a46eb6a8bab5fb69584bb7c983c499ea3d4783
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375106"
---
# <a name="choosing-the-32-bit-or-64-bit-debugging-tools"></a>选择 32 位或 64 位调试工具


安装的 Windows 调试工具，可以获取两个 32 位套工具和 64 位一系列工具。 如果你使用 Microsoft Visual Studio[调试环境](debuggers-in-the-debugging-tools-for-windows-package.md)，无需担心是否使用 32 位或 64 位设置，因为 Visual Studio 会自动选择正确的调试工具。

如果使用其他调试环境 （WinDbg、 KD、 CDB 或 NTSD），您必须自己做出的选择。 若要确定要使用的调试工具集，您需要知道的主机计算机和主机计算机是否运行 Windows 的 32 位或 64 位版本运行的处理器的类型。

运行调试器的计算机称为*主机计算机*，和正在调试的计算机称为*目标计算机*。

### <a name="span-idhostcomputerrunninga32-bitversionofwindowsspanspan-idhostcomputerrunninga32-bitversionofwindowsspanspan-idhostcomputerrunninga32-bitversionofwindowsspanhost-computer-running-a-32-bit-version-of-windows"></a><span id="Host_computer_running_a_32-bit_version_of_Windows"></span><span id="host_computer_running_a_32-bit_version_of_windows"></span><span id="HOST_COMPUTER_RUNNING_A_32-BIT_VERSION_OF_WINDOWS"></span>运行 Windows 的 32 位版本的主机计算机

如果在主计算机正在运行 Windows 的 32 位版本，使用 32 位调试工具。 （这种情况下适用于基于 x86 和基于 x64 的目标。）

### <a name="span-idx64-basedhostcomputerrunninga64-bitversionofwindowsspanspan-idx64-basedhostcomputerrunninga64-bitversionofwindowsspanspan-idx64-basedhostcomputerrunninga64-bitversionofwindowsspanx64-based-host-computer-running-a-64-bit-version-of-windows"></a><span id="x64-based_host_computer_running_a_64-bit_version_of_Windows"></span><span id="x64-based_host_computer_running_a_64-bit_version_of_windows"></span><span id="X64-BASED_HOST_COMPUTER_RUNNING_A_64-BIT_VERSION_OF_WINDOWS"></span>基于 x64 的主机计算机运行 Windows 的 64 位版本

如果主机计算机使用的基于 x64 的处理器和正在运行 Windows 的 64 位版本，适用以下规则：

-   如果您正在分析转储文件，可以使用的调试工具会 32 位或 64 位调试工具。 （它并不重要转储文件是否为用户模式转储文件或内核模式转储文件，并将它并不重要的转储文件是否生成了基于 x86 或基于 x64 的平台上。）

-   如果您正在执行实时内核模式调试，可以使用 32 位调试工具或进行 x64 调试工具。 （这种情况下适用于基于 x86 和基于 x64 的目标。）

-   如果调试在调试器所在的计算机运行的实时用户模式代码时，使用 64 位工具调试 64 位代码和在 WOW64 上运行的 32 位代码。 若要为 32 位或 64 位模式对调试器进行设置，请使用[ **.effmach** ](-effmach--effective-machine-.md)命令。

-   如果你正在调试的单独的目标计算机运行的实时的 32 位用户模式代码，使用 32 位调试工具。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[Windows 调试](index.md)

 

 







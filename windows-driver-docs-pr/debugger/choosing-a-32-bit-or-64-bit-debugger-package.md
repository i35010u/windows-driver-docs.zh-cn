---
title: 选择 32 位或 64 位调试工具
description: 当你安装适用于 Windows 的调试工具时，你将获得32位工具集和一组64工具。
keywords:
- 32位调试器包
- 32位调试工具
- 64位调试器包
- 64位调试工具
- 安装，在32位和64位包之间选择
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f289ef076d6ee149231a27abd50e50d87c1a36f7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821605"
---
# <a name="choosing-the-32-bit-or-64-bit-debugging-tools"></a>选择 32 位或 64 位调试工具


当你安装适用于 Windows 的调试工具时，你将获得32位工具集和一组64工具。

如果使用的是其他调试环境之一 (WinDbg、KD、CDB 或 NTSD) ，则必须自行做出选择。 若要确定要使用的调试工具集，需要知道主机计算机上运行的处理器的类型，以及主计算机运行的是32还是64位版本的 Windows。

运行调试器的计算机称为 *主机计算机*，被调试的计算机称为 *目标计算机*。

### <a name="span-idhost_computer_running_a_32-bit_version_of_windowsspanspan-idhost_computer_running_a_32-bit_version_of_windowsspanspan-idhost_computer_running_a_32-bit_version_of_windowsspanhost-computer-running-a-32-bit-version-of-windows"></a><span id="Host_computer_running_a_32-bit_version_of_Windows"></span><span id="host_computer_running_a_32-bit_version_of_windows"></span><span id="HOST_COMPUTER_RUNNING_A_32-BIT_VERSION_OF_WINDOWS"></span>运行32位版本 Windows 的主机计算机

如果您的主计算机运行的是32位版本的 Windows，请使用32位调试工具。  (这种情况适用于基于 x86 和基于 x64 的目标。 ) 

### <a name="span-idx64-based_host_computer_running_a_64-bit_version_of_windowsspanspan-idx64-based_host_computer_running_a_64-bit_version_of_windowsspanspan-idx64-based_host_computer_running_a_64-bit_version_of_windowsspanx64-based-host-computer-running-a-64-bit-version-of-windows"></a><span id="x64-based_host_computer_running_a_64-bit_version_of_Windows"></span><span id="x64-based_host_computer_running_a_64-bit_version_of_windows"></span><span id="X64-BASED_HOST_COMPUTER_RUNNING_A_64-BIT_VERSION_OF_WINDOWS"></span>运行64位版本 Windows 的基于 x64 的主机计算机

如果您的主计算机使用基于 x64 的处理器，并且运行64位版本的 Windows，则以下规则适用：

- 如果要分析转储文件，可以使用32位调试工具或64位调试工具。  (转储文件是用户模式转储文件还是内核模式转储文件并不重要，不管转储文件是在基于 x86 的平台上还是基于 x64 的平台上进行的，都不重要。 ) 

- 如果要执行实时内核模式调试，则可以使用32位调试工具或 x64 调试工具。  (这种情况适用于基于 x86 和基于 x64 的目标。 ) 

- 如果调试的是与调试器在同一台计算机上运行的实时用户模式代码，请使用64位工具调试在 WOW64 上运行的64位代码和32位代码。 若要将调试器设置为32位或64位模式，请使用 [**effmach**](-effmach--effective-machine-.md) 命令。

- 如果要调试在单独的目标计算机上运行的实时32位用户模式代码，请使用32位调试工具。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[Windows 调试](index.md)

---
title: 强制执行内核模式中的内核调试的签名验证
description: 介绍如何附加内核调试程序时启用强制加载时签名。
ms.assetid: D7CB436F-4B89-49E7-BB53-101BDA7046F3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 482bf6685c401dba51b1c405448642271aec85f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385558"
---
# <a name="appendix-1-enforcing-kernel-mode-signature-verification-in-kernel-debugging-mode"></a>附录 1：强制在内核调试模式下进行内核模式签名验证


## <a name="enforcing-kernel-mode-signature-verification-in-kernel-debugging-mode"></a>强制在内核调试模式下进行内核模式签名验证


*从节选*[开发和测试期间安装未签名的驱动程序](installing-an-unsigned-driver-during-development-and-test.md):

在某些情况下，开发人员可能需要附加内核调试程序时启用强制加载时签名。 此示例是当驱动程序堆栈具有的未签名的驱动程序 （例如筛选器驱动程序） 无法加载，这可能会使整个堆栈。 由于附加调试程序允许加载未签名驱动程序，将出现此问题已附加调试器时，就立即消失。 调试此类问题可能很难。

为了便于调试这类情况下，内核模式代码签名策略支持以下注册表值：

```cpp
HKLM\SYSTEM\CurrentControlSet\Control\CI\DebugFlags
```

此注册表值为类型[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)，并且可以分配基于一个或多个下列标志的按位 OR 的值。

```cpp
0x00000001
```

此标志值配置中断调试器，如果驱动程序是无符号的内核。 开发人员或测试人员然后可以选择通过输入 g 调试器提示符下，加载未签名的驱动程序。

```cpp
0x00000010
```

此标志值将配置为忽略调试器存在并将始终阻止加载未签名驱动程序的内核。

如果此注册表值在注册表中不存在或不基于前面所述的标志的值，内核将始终加载内核调试模式，而无论是否签名驱动程序中的驱动程序。

**请注意**  此注册表值中不存在注册表默认情况下。 若要调试内核模式签名验证，必须创建值。

 

 

 






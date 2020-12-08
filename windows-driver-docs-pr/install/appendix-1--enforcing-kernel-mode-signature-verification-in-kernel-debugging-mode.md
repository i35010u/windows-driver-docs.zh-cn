---
title: 在内核调试中强制执行 Kernel-Mode 签名验证
description: 描述如何在附加内核调试器时启用加载时签名强制。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83d6c1ac8ac60df286ad7ae423a058a1358ac810
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803851"
---
# <a name="appendix-1-enforcing-kernel-mode-signature-verification-in-kernel-debugging-mode"></a>附录 1：强制在内核调试模式下进行内核模式签名验证


## <a name="enforcing-kernel-mode-signature-verification-in-kernel-debugging-mode"></a>强制在内核调试模式下进行内核模式签名验证


在 [开发和测试过程中安装未签名驱动程序](installing-an-unsigned-driver-during-development-and-test.md)*的摘录*：

在某些情况下，开发人员在连接内核调试器时可能必须启用加载时签名。 例如，当驱动程序堆栈具有未签名的驱动程序 (例如无法加载的筛选器驱动程序) 时，这可能会使整个堆栈失效。 由于附加调试器允许加载未签名的驱动程序，因此，一旦附加调试器，问题就会消失。 调试此类问题可能比较困难。

为了便于调试这些情况，内核模式代码签名策略支持以下注册表值：

```cpp
HKLM\SYSTEM\CurrentControlSet\Control\CI\DebugFlags
```

此注册表值的类型为 [REG_DWORD](/windows/desktop/SysInfo/registry-value-types)，可以根据一个或多个以下标志的按位 "或" 赋值。

```cpp
0x00000001
```

此标志值将内核配置为在驱动程序未签名时中断到调试器。 然后，开发人员或测试人员可以通过在调试器提示符下输入 g 来选择加载未签名的驱动程序。

```cpp
0x00000010
```

此标志值将内核配置为忽略调试器的状态，并始终阻止未签名的驱动程序加载。

如果注册表中不存在此注册表值，或者其值不基于前面所述的标志，则内核将始终在内核调试模式下加载驱动程序，而不管驱动程序是否已签名。

**注意**  默认情况下，注册表中不存在此注册表值。 必须创建值才能调试内核模式签名验证。

 

 


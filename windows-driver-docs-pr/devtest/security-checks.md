---
title: 安全检查
description: 安全检查
ms.assetid: fca92bad-7bb8-4a30-b303-48fd54c20c42
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fb12bfe53650e83e04e9eb5e4d8adf25921dad7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340137"
---
# <a name="security-checks"></a>安全检查


驱动程序验证程序的安全检查选项可监视可能会导致安全漏洞的常见错误的驱动程序。 此选项才可用在 Windows Vista 中启动。

具体而言，安全检查选项中查找以下不正确的驱动程序行为：

- **作为参数调用内核 ZwXxx 例程使用用户模式地址。** 当驱动程序调用任何**Zw * Xxx*** 例程，驱动程序验证程序检查所有参数是否是用户模式地址。 当调用任何**Zw * Xxx*** 例程，当前 KPROCESSOR\_模式下会变成**KernelMode**，和任何参数传递给例程将其视为好像它们是内核模式地址。 因此，该驱动程序必须探测从应用程序收到任何用户模式缓冲区并在调用内核之前将其放入内核模式 （例如，在内核堆栈上分配的池块或数据结构） 的内存**Zw * Xxx***例程。 该驱动程序必须使用捕获的缓冲区而不是用户模式缓冲区作为参数的**Zw * Xxx*** 例程。

- **调用内核 ZwXxx 例程使用格式不正确的 UNICODE\_字符串作为参数。** 当驱动程序调用任何**Zw * Xxx*** 例程，驱动程序验证工具将检查任何参数属于 UNICODE\_字符串值。 在此类字符串中的驱动程序验证程序检测到的常见错误包括：
  -   **缓冲区字段指向用户模式内存中。**
  -   **长度或 MaximumLength 参数不正确。** 例如， *MaximumLength* &lt; *长度*。 或一个或两个这些值的个数为奇数。 两者的值必须始终为甚至因为它们代表用于表示一个 Unicode 字符串的字节数。
- **调用具有不正确的对象的内核 ZwXxx 例程\_属性结构作为参数。** 当驱动程序调用任何**Zw * Xxx*** 例程，驱动程序验证工具将检查对象的所有参数\_属性结构。 每个对象的成员\_特性结构参数受制于相同的检查用户模式地址和 UNICODE\_上面所述的字符串值。

- **不一致 Irp-&gt;RequestorMode 和 I/O 请求参数。** 每当**Irp-&gt; RequestorMode**设置为**KernelMode**，驱动程序验证程序检查任何 I/O 请求参数， **Irp-&gt;AssociatedIrp.SystemBuffer**或**Irp-&gt;UserBuffer**，是用户模式地址。

如果启用任何 Driver Verifier 选项从其开始使用 Windows 7，驱动程序验证程序检查存在以下驱动程序行为：

**对象引用计数器从 0 更改为 1。**
当 Windows 内核对象管理器创建一个对象，如文件对象或线程对象，该新对象的引用计数器设置为 1。 调用系统函数如[ **ObReferenceObjectByPointer** ](https://msdn.microsoft.com/library/windows/hardware/ff558686)或[ **ObReferenceObjectByHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff558679)递增引用计数器。 每次调用[ **ObDereferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff557724)为相同的对象的引用计数器递减。

引用计数器值达到 0 的值后，该对象将成为以便释放。 对象管理器可能会立即释放它或更高版本可能会释放。 驱动程序验证工具以便后续调用将检查[ **ObReferenceObjectByPointer** ](https://msdn.microsoft.com/library/windows/hardware/ff558686)并[ **ObReferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff558678)为同一对象。 这些调用将引用计数器从 0 更改为 1，这意味着该驱动程序时已释放对象的引用计数器递增。 这是始终不正确，因为它可能会破坏其他内存分配。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

可以使用驱动程序验证程序管理器或 Verifier.exe 命令行来激活一个或多个驱动程序的安全检查选项。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。

-   **使用命令行**

    在命令行中，由表示的安全检查的选项**位 8 (0x100)** 。 若要激活安全检查，使用 0x100 标志值，或将 0x100 添加到标志值。 例如：

    ```
    verifier /flags 0x100 /driver MyDriver.sys
    ```

    重启计算机后，该选项将处于活动状态。

    从 Windows Vista 开始，你可以还激活和停用安全检查而无需重新启动计算机，通过添加 **/volatile**命令参数。 例如：

    ```
    verifier /volatile /flags 0x100 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时将丢失。 有关详细信息，请参阅[使用易失性设置](using-volatile-settings.md)。

    安全检查选项也包含在标准设置。 例如：

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **使用驱动程序验证程序管理器**

    1.  启动驱动程序验证器管理器。 类型**Verifier**在命令提示符窗口中。
    2.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步**。
    3.  选择**从完整的列表中选择单个设置**。
    4.  选择**安全检查**。

    安全检查功能也包含在标准设置。 若要使用此功能在驱动程序验证程序管理器中，单击**创建标准设置**。

 

 






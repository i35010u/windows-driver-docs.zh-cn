---
title: 安全检查
description: 安全检查
ms.assetid: fca92bad-7bb8-4a30-b303-48fd54c20c42
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 205ac99627c83a5cfc3217e2e68477896d629d87
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840042"
---
# <a name="security-checks"></a>安全检查


驱动程序验证程序的 "安全检查" 选项监视驱动程序是否存在可能导致安全漏洞的常见错误。 从 Windows Vista 开始，此选项可用。

具体而言，"安全检查" 选项将查找以下不正确的驱动程序行为：

- **将用户模式地址的内核 ZwXxx 例程作为参数调用。** 当驱动程序调用任何**Zw * Xxx*** 例程时，驱动程序验证器将检查任何参数都不是用户模式的地址。 如果调用任何**Zw * Xxx*** 例程，则当前的 KPROCESSOR\_模式将变为**KernelMode**，并且传递到该例程的任何参数都将被视为内核模式地址。 因此，该驱动程序必须探测从应用程序接收的任何用户模式缓冲区，并将其放入内核模式内存（例如，在池块中，或者在内核堆栈上分配的数据结构中），然后再调用内核**Zw * Xxx*** 例程。 驱动程序必须使用捕获的缓冲区而不是用户模式缓冲区作为**Zw * Xxx*** 例程的参数。

- **调用\_字符串格式不正确的内核 ZwXxx 例程作为参数。** 当驱动程序调用任何**Zw * Xxx*** 例程时，驱动程序验证器将检查任何 UNICODE 参数\_字符串值。 驱动程序验证程序检测到的常见错误包括：
  -   **缓冲区字段指向用户模式内存。**
  -   **长度或 MaximumLength 参数不正确。** 例如， *MaximumLength* &lt;*长度*。 或者这两个值中的一个或两个都是奇数。 这两个值必须始终为偶数，因为它们表示用于表示 Unicode 字符串的字节数。
- **使用错误的对象\_特性结构调用内核 ZwXxx 例程作为参数。** 当驱动程序调用任何**Zw * Xxx*** 例程时，驱动程序验证器将检查作为 OBJECT\_属性结构的所有参数。 每个对象\_属性结构参数的成员对用户模式地址和 UNICODE\_上述字符串值进行相同的检查。

- **Irp&gt;Irp->requestormode 和 i/o 请求参数不一致。** 每当将**Irp&gt; irp->requestormode**设置为**KernelMode**时，驱动程序验证器将检查没有 I/o 请求参数、 **irp&gt;AssociatedIrp**或**irp&gt;UserBuffer**，它们都是用户模式的地址。

从 Windows 7 开始，当你启用任何驱动程序验证程序选项时，驱动程序验证程序将检查以下驱动程序行为：

**对象引用计数器从0更改为1。**
当 Windows 内核对象管理器创建对象（如文件对象或线程对象）时，新对象的引用计数器将设置为1。 对系统函数（如[**ObReferenceObjectByPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer)或[**ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle) ）的调用递增了引用计数器。 对同一对象的[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)的每次调用都会减少引用计数器。

引用计数器达到0值后，就可以释放对象了。 对象管理器可能会立即释放该对象，否则以后可能会将其释放。 驱动程序验证程序检查对同一对象的[**ObReferenceObjectByPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer)和[**ObReferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)的后续调用。 这些调用将引用计数器从0更改为1，这意味着驱动程序已增加已经释放的对象的引用计数器。 这始终不正确，因为它可能会损坏其他内存分配。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

您可以使用驱动程序验证器管理器或 Verifier 命令行为一个或多个驱动程序激活安全检查选项。 有关详细信息，请参阅[选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。

-   **使用命令行**

    在命令行中，安全检查选项由**第8位（0x100）** 表示。 若要激活安全检查，请使用0x100 的标志值或将0x100 添加到标志值。 例如：

    ```
    verifier /flags 0x100 /driver MyDriver.sys
    ```

    重新启动计算机后，此选项将处于活动状态。

    从 Windows Vista 开始，你还可以通过将 **/volatile**参数添加到命令来激活和停用安全检查，而无需重新启动计算机。 例如：

    ```
    verifier /volatile /flags 0x100 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时，此设置会丢失。 有关详细信息，请参阅[使用可变设置](using-volatile-settings.md)。

    标准设置中也包括 "安全检查" 选项。 例如：

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **使用驱动程序验证器管理器**

    1.  启动驱动程序验证器管理器。 在命令提示符窗口中键入**Verifier** 。
    2.  选择 "**创建自定义设置（适用于代码开发人员）** "，然后单击 "**下一步**"。
    3.  选择 "**从完整列表中选择单个设置**"。
    4.  选择 "**安全检查**"。

    标准设置中也包含安全检查功能。 若要在驱动程序验证器管理器中使用此功能，请单击 "**创建标准设置**"。

 

 






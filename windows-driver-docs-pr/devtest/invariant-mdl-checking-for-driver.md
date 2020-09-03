---
title: 针对驱动程序的固定 MDL 检查
description: 面向驱动程序的固定 MDL 检查选项用于监控每个驱动程序是如何处理固定 MDL 缓冲区的。
ms.assetid: 2FA69B7C-3EF4-4660-84D4-5108C97E395F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d03abfdb3be6a8e708c34ccb48ba1aac1953d71
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384553"
---
# <a name="invariant-mdl-checking-for-driver"></a>针对驱动程序的固定 MDL 检查


面向驱动程序的固定 MDL 检查选项用于监控每个驱动程序是如何处理固定 MDL 缓冲区的。 此选项可检测是否对固定 MDL 缓冲区进行了非法修改。 若要使用此选项，你必须在至少一个驱动程序上启用 I/O 验证。

**注意**   从 Windows 8 开始可以使用此选项。

 

"对驱动程序进行固定 MDL 检查" 选项执行的固定 MDL 检查形式比 " [固定 Mdl 检查堆栈](invariant-mdl-checking-for-stack.md) " 选项更密集。 当驱动程序的固定 MDL 检查处于活动状态时，将跨每次调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 和 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 例程来验证缓冲区不变性。

每次使用 IRP 查看新的固定 MDL 缓冲区时，驱动程序验证器会计算缓冲区内容的签名，并将其存储在其内部数据库中。 当驱动程序验证器遇到先前已出现的固定 MDL 缓冲区时，它通过将数据库中的签名与通过当前固定 MDL 缓冲区内容计算的签名进行比较来验证缓冲区的内容是否未更改。

此选项是全局性的，不能有选择地强制实施某些驱动程序。

## <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项


可以通过使用驱动程序验证器管理器或 Verifier.exe 命令行为一个或多个驱动程序激活固定 MDL 检查驱动程序功能。 有关详细信息，请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。 您必须重新启动计算机以激活或停用 "驱动程序的固定 MDL 检查" 选项。

若要激活 [固定 MDL 检查堆栈](invariant-mdl-checking-for-stack.md) 选项，还必须激活 [i/o 验证](i-o-verification.md)。

-   **在命令行中**

    在命令行中，驱动程序的固定 MDL 检查由 **verifier/flags 0x00004000** (位 14) 表示。 若要为驱动程序激活固定 MDL 检查，请使用0x00004010 的标志值或将0x00004010 添加到标志值。 此值为驱动程序 (0x00004000)  (0x10) 和固定 MDL 检查启用 i/o 验证。 例如：

    ```
    verifier /flags 0x00004010 /driver MyDriver.sys
    ```

    此功能将在下一次启动后处于活动状态。

-   **使用驱动程序验证器管理器**
    1.  启动驱动程序验证器管理器。 在命令提示符窗口中键入 **Verifier** 。
    2.  选择 " **为代码开发人员 (创建自定义设置") ** ，然后单击 " **下一步"。**
    3.  选择 " **从完整列表中选择单个设置**"。
    4.  选择 (检查是否有驱动程序) [I/o 验证](i-o-verification.md) 和固定 MDL 检查。
    5.  重新启动计算机。

 


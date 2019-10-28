---
title: 针对堆栈的固定 MDL 检查
description: "\"固定 MDL 检查堆栈\" 选项监视驱动程序如何处理驱动程序堆栈间的固定 MDL 缓冲区。"
ms.assetid: AB27803A-6B3A-40FA-B962-79B0DA2F5FA9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 126ea493f4fb2f81179d5d983c511b47e4bd7963
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840262"
---
# <a name="invariant-mdl-checking-for-stack"></a>针对堆栈的固定 MDL 检查


"固定 MDL 检查堆栈" 选项监视驱动程序如何处理驱动程序堆栈间的固定 MDL 缓冲区。 驱动程序验证程序可检测是否对固定 MDL 缓冲区进行了非法修改。 若要使用此选项，必须在至少一个驱动程序上启用 I/O 验证。

**请注意**  此选项可从 Windows 8 开始使用。

 

"固定 MDL 检查堆栈" 选项可确保驱动程序仅在请求离开驱动程序堆栈时遵循固定 MDL 缓冲区的规则。

第一次在[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)例程中会出现具有固定 MDL 的 IRP 时，将从固定 mdl 缓冲区的内容计算出唯一的签名，并将其存储在内部数据库中。 在[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)例程中完成 irp 的过程中，如果 irp 仍具有我们为其记录签名的固定 MDL，则驱动程序验证程序将验证缓冲区是否已更改。

对于写入请求，不能在 IRP 的整个生存期内修改固定缓冲区。 对于读取请求，无法在其调度路径上修改固定缓冲区，因此，在对[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)的最后一次调用时，将对缓冲区签名进行比较。

"针对堆栈的固定 MDL 检查" 选项在整个驱动程序堆栈中验证 MDL 缓冲区不变性，而不考虑缓冲区在堆栈中通过各个驱动程序时所发生的情况。 此选项是全局性的，不能在每个驱动程序的基础上有选择地执行。 "对堆栈进行固定 MDL 检查" 选项只能捕获冲突，而不能找出违反缓冲区不变性的驱动程序。 若要帮助查明错误的驱动程序，请使用 "[固定 MDL 检查驱动程序](invariant-mdl-checking-for-driver.md)" 选项，该选项可在每次调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)和[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) DDIs 时验证缓冲区内容的不变性。

## <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项


可以通过使用驱动程序验证器管理器或 Verifier 命令行为一个或多个驱动程序激活固定 MDL 检查堆栈功能。 您必须重新启动计算机以激活或停用针对 Stack 的固定 MDL 检查选项。 有关详细信息，请参阅[选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。

若要激活固定 MDL 检查堆栈选项，还必须激活[I/o 验证](i-o-verification.md)。

-   **在命令行中**

    在命令行中，堆栈的固定 MDL 检查由**0x00002000** （第13位）表示。 若要为堆栈激活固定 MDL 检查，请使用0x00002010 标志值或将0x00002010 添加到标志值。 此值为 Stack 激活 i/o 验证（0x10）和固定 MDL 检查（0x00002000）。 例如：

    ```
    verifier /flags 0x00002010 /driver MyDriver.sys
    ```

    此功能将在下一次启动后处于活动状态。

-   **使用驱动程序验证器管理器**
    1.  启动驱动程序验证器管理器。 在命令提示符窗口中键入**Verifier** 。
    2.  选择 "**创建自定义设置（对于代码开发人员）** "，然后单击 "**下一步"。**
    3.  选择 "**从完整列表中选择单个设置**"。
    4.  选择（检查）堆栈的[I/o 验证](i-o-verification.md)和固定 MDL 检查。
    5.  重新启动计算机。

 

 






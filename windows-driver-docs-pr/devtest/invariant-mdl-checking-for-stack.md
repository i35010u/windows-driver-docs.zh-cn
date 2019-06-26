---
title: 面向堆栈的固定 MDL 检查
description: 固定 MDL 检查堆栈选项监视驱动程序如何跨驱动程序堆栈处理固定 MDL 缓冲区。
ms.assetid: AB27803A-6B3A-40FA-B962-79B0DA2F5FA9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 173c8e9266184942287b4d588479275bd56566e0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373710"
---
# <a name="invariant-mdl-checking-for-stack"></a>面向堆栈的固定 MDL 检查


固定 MDL 检查堆栈选项监视驱动程序如何跨驱动程序堆栈处理固定 MDL 缓冲区。 驱动程序验证程序可检测是否对固定 MDL 缓冲区进行了非法修改。 若要使用此选项，必须在至少一个驱动程序上启用 I/O 验证。

**请注意**  此选项才可用从 Windows 8 开始。

 

固定 MDL 检查的堆栈选项可确保驱动程序遵循的规则，用于固定 MDL 缓冲区只能在点请求将脱离驱动程序堆栈。

第一次使用固定 MDL 示 IRP [ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)例程，唯一的签名是从固定 MDL 缓冲区的内容计算和存储在内部数据库中。 期间完成中 IRP [ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)缓冲区未更改的例程，如果 IRP 仍包含我们记录其签名，固定 MDL 驱动程序验证程序验证。

固定缓冲区，用于写入请求，不能修改整个 IRP 的整个生存期。 对于读取请求，固定缓冲区无法修改其调度路径，以便在上次调用完成的缓冲区签名进行比较[ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)。

固定 MDL 检查堆栈选项验证 MDL 缓冲区不变性跨整个驱动程序堆栈，而不考虑将在堆栈中的单个驱动程序通过传递，该缓冲区会发生什么情况。 此选项是全局的并且不能有选择地强制实施在每个驱动程序的基础上。 固定 MDL 检查堆栈选项仅可以捕获该冲突，而不需要能够准确找出违反缓冲区不变性的驱动程序。 若要帮助找出错误的驱动程序，请使用[驱动程序检查固定 MDL](invariant-mdl-checking-for-driver.md)选项，将在每次调用上执行验证的不变性缓冲区的内容[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)并[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) DDIs。

## <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项


可以使用驱动程序验证程序管理器或 Verifier.exe 命令行激活固定 MDL 检查一个或多个驱动程序的堆栈功能。 必须重新启动计算机以激活或停用固定 MDL 检查堆栈选项。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。

若要激活固定 MDL 检查堆栈选项，你必须激活[I/O 验证](i-o-verification.md)。

-   **在命令行**

    在命令行中，在由表示为堆栈检查固定 MDL **0x00002000** (位 13)。 若要激活 MDL 堆栈检查不变，使用 0x00002010 标志值，或将 0x00002010 添加到标志值。 此值将激活的 I/O 验证 (0x10) 和固定 MDL 正在检查堆栈 (0x00002000)。 例如：

    ```
    verifier /flags 0x00002010 /driver MyDriver.sys
    ```

    在下一次启动后，该功能将处于活动状态。

-   **使用驱动程序验证程序管理器**
    1.  启动驱动程序验证器管理器。 类型**Verifier**在命令提示符窗口中。
    2.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步。**
    3.  选择**从完整的列表中选择单个设置**。
    4.  选择 （选中） [I/O 验证](i-o-verification.md)和 MDL 堆栈检查不变。
    5.  重新启动计算机。

 

 






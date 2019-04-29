---
title: 面向驱动程序的固定 MDL 检查
description: 固定 MDL 检查驱动程序选项监视驱动程序如何处理在每个驱动程序的基础上的固定 MDL 缓冲区。
ms.assetid: 2FA69B7C-3EF4-4660-84D4-5108C97E395F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87a4da5d4efe8b8d26ea6fdf77a3b6897d240a4b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356533"
---
# <a name="invariant-mdl-checking-for-driver"></a>面向驱动程序的固定 MDL 检查


固定 MDL 检查驱动程序选项监视驱动程序如何处理在每个驱动程序的基础上的固定 MDL 缓冲区。 此选项可检测是否对固定 MDL 缓冲区进行了非法修改。 若要使用此选项，你必须在至少一个驱动程序上启用 I/O 验证。

**请注意**  此选项才可用从 Windows 8 开始。

 

固定 MDL 检查驱动程序选项执行更密集的窗体的比检查固定 MDL [MDL 堆栈检查固定](invariant-mdl-checking-for-stack.md)选项。 当驱动程序的固定 MDL 检查处于活动状态时，在每次调用之间验证缓冲区不变性[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)并[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)例程。

每次使用 IRP 时出现一个新的固定 MDL 缓冲区，驱动程序验证程序计算的缓冲区内容签名，并将其存储在其内部数据库中。 当驱动程序验证程序遇到它具有前面介绍的固定 MDL 缓冲区时，它将验证该缓冲区的内容未更改，通过比较在数据库中具有对当前固定 MDL 缓冲区内容计算签名的签名。

此选项是全局设置，不能有选择地强制实施某些驱动程序。

## <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项


可以使用驱动程序验证程序管理器或 Verifier.exe 命令行激活一个或多个驱动程序的驱动程序功能的固定 MDL 检查。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。 必须重新启动计算机以激活或停用固定 MDL 检查驱动程序选项。

若要激活[MDL 堆栈检查固定](invariant-mdl-checking-for-stack.md)选项，也必须激活[I/O 验证](i-o-verification.md)。

-   **在命令行**

    在命令行中，在由表示驱动程序检查固定 MDL **verifier /flags 0x00004000** (位 14)。 若要激活固定 MDL 检查驱动程序，使用 0x00004010 标志值，或将 0x00004010 添加到标志值。 此值将激活的 I/O 验证 (0x10) 和固定 MDL 检查驱动程序 (0x00004000)。 例如：

    ```
    verifier /flags 0x00004010 /driver MyDriver.sys
    ```

    在下一次启动后，该功能将处于活动状态。

-   **使用驱动程序验证程序管理器**
    1.  启动驱动程序验证器管理器。 类型**Verifier**在命令提示符窗口中。
    2.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步。**
    3.  选择**从完整的列表中选择单个设置**。
    4.  选择 （选中）[I/O 验证](i-o-verification.md)和固定 MDL 检查驱动程序。
    5.  重新启动计算机。

 

 






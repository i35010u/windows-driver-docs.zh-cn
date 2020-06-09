---
title: 调试设备安装包中的辅助安装程序
description: 调试设备安装包中的辅助安装程序
ms.assetid: a5cf3cec-bd61-49a6-b836-6759cd8c7d82
keywords:
- 设备安装共同安装程序调试
- 安装共同安装程序调试
- 共同安装程序调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 734987cb7b563937f489d20c3caeaa75296c66bf
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534782"
---
# <a name="debugging-a-device-installation-co-installer"></a>调试设备安装包中的辅助安装程序


## <span id="ddk_debugging_dual_boot_machines_dbg"></span><span id="DDK_DEBUGGING_DUAL_BOOT_MACHINES_DBG"></span>


某些硬件设备安装包包括称为*共同安装程序*的 DLL 文件，这有助于安装设备。

不能以与其他模块相同的方式调试共同安装程序。 这是因为加载共同安装程序的方法是独特的，因为许多安装方案会自动发生，而不会让开发人员中断正在运行的进程。

可以通过编程方式安装设备来解决此问题。 将调试器附加到安装了设备的应用程序后，可以访问共同安装程序本身。 实现此目的的最简单方法是使用 Windows 驱动程序工具包（WDK）中包含的[DevCon](https://docs.microsoft.com/windows-hardware/drivers/devtest/devcon)工具来安装或重新安装该设备。 然后，您可以用 WinDbg 调试共同安装程序。

使用以下过程来完成此任务。 此过程假定你已为使用共同安装程序的设备开发了一个工作的驱动程序安装包。 它还假定您拥有最新的 WDK 副本。 有关开发驱动程序、驱动程序安装包和驱动程序安装共同安装程序的信息，请参阅 WDK 文档。

**使用 DevCon 和 WinDbg 调试共同安装程序**

1.  插入硬件设备。

2.  取消 "**发现新硬件**" 向导。

3.  启动 WinDbg。

4.  从 WinDbg 的 "文件" 菜单中选择 "**打开可执行****文件**"。

5.  在 "**打开可执行文件**" 对话框中，执行以下操作：
    1.  在 "文件选择" 文本框中，选择 DevCon 工具（Devcon）。 为此，请浏览到 WDK 安装文件夹，然后打开 "子目录" 工具，打开子目录 "devcon"，打开与计算机的处理器体系结构匹配的子目录，然后选择 "Devcon"。 在 Devcon .exe 上单击一次，但不要按 "**打开**"。
    2.  在 "**参数**" 文本框中，输入以下文本，其中*INFFile*是设备安装信息（INF）文件的文件名， *HARDWAREID*是设备的硬件 ID：

        ```text
        update INFFile HardwareID 
        ```

    3.  在 "**开始目录**" 文本框中，输入设备安装包的路径。
    4.  单击“打开” 。

6.  调试过程将开始，并且在 DevCon 安装您的驱动程序之前，WinDbg 会中断 DevCon 进程。

7.  将调试器配置为在加载时中断共同安装程序进程。 可以通过以下方法之一来执行此操作：
    -   在调试器命令窗口中，使用后跟**ld：** 的[**Sxe （Set 例外）**](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)命令，然后使用共同安装程序的文件名（不包括文件扩展名）。 冒号后面应没有空格。例如，如果共同安装程序的名称为 mycoinst，则可以使用以下命令：
        ```dbgcmd
        sxe ld:mycoinst 
        ```

    -   从 WinDbg 的 "**调试**" 菜单中选择 "**事件筛选器**"。 在 "**事件筛选器**" 对话框中，选择 "**加载模块**"。 在 "**执行**" 下，选择 "**已启用"。** 在 "**继续**" 下，选择 "**未处理"。** 单击 "**参数**" 按钮，然后在文本框中输入共同安装程序的文件名（不包括文件扩展名）（例如，为 mycoinst 输入 "mycoinst"）。 单击 **"确定"** ，然后单击 "**关闭**"。

8.  按 F5 或在调试器命令窗口中输入**g （中转）** 命令，继续执行。

9.  加载共同安装程序后，执行将会重新进入调试器。 此时，你可以设置所需的任何其他断点。

### <a name="span-idlimitations_of_this_procedurespanspan-idlimitations_of_this_procedurespanlimitations-of-this-procedure"></a><span id="limitations_of_this_procedure"></span><span id="LIMITATIONS_OF_THIS_PROCEDURE"></span>此过程的限制

在某些情况下，在 DevCon 下运行设备安装包可能会导致与 PnP 安装的行为稍有不同，因为不同的安全令牌和类似的安全令牌。 如果你尝试调试共同安装程序中的特定问题，则在涉及 DevCon 的情况下，此问题可能不会复制。 因此，在使用此方法之前，应使用 DevCon 来安装没有附加调试器的驱动程序，以验证此问题是否存在于 PnP 和 DevCon 方案中。

如果在 DevCon 启动安装时消失问题，则必须在不使用 DevCon 的情况下调试你的共同安装程序。 执行此操作的一种方法是将[tlist.exe](tlist.md)工具与 **/m**选项一起使用，以确定哪个进程正在加载共同安装程序模块，然后将调试器附加到该进程。

 

 






---
title: 调试设备安装包中的辅助安装程序
description: 调试设备安装包中的辅助安装程序
ms.assetid: a5cf3cec-bd61-49a6-b836-6759cd8c7d82
keywords:
- 设备安装共同安装程序调试
- 安装辅助安装程序调试
- 调试共同安装程序
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce340d98e111ff1bf87b7877c402ae54b8afff22
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324639"
---
# <a name="debugging-a-device-installation-co-installer"></a>调试设备安装包中的辅助安装程序


## <span id="ddk_debugging_dual_boot_machines_dbg"></span><span id="DDK_DEBUGGING_DUAL_BOOT_MACHINES_DBG"></span>


一些硬件设备安装包中包含 DLL 文件称为*共同安装程序*，该设备的安装帮助。

不能调试相同方式与其他模块的共同安装程序。 这是因为所在加载，辅助安装程序的唯一方式是，因为无需提供开发人员可以分解为正在运行的进程会自动执行各种安装方案。

可以通过以编程方式安装在设备来解决此问题。 将调试器附加到应用程序安装在设备允许访问共同安装程序本身。 实现此目的的最简单方法是安装或重新安装设备使用[DevCon](https://go.microsoft.com/fwlink/p/?linkid=152915)包括 Windows Driver Kit (WDK) 中的工具。 然后可以共同安装程序使用 WinDbg 进行调试。

使用以下过程来完成此任务。 此过程假定您已为你的设备使用共同安装程序的开发工作驱动程序安装包。 它还假定您有 WDK 的最新副本。 开发驱动程序、 驱动程序安装包和驱动程序安装共同安装程序的信息，请参阅 WDK 文档。

**调试共同安装程序使用 DevCon 和 WinDbg**

1.  插入硬件设备。

2.  取消**发现新硬件**向导。

3.  启动 WinDbg。

4.  选择**打开可执行文件**WinDbg 的从**文件**菜单。

5.  在中**打开可执行文件**对话框框中，执行以下操作：
    1.  在文件选择文本框中，选择 DevCon 工具 (Devcon.exe)。 为此中,，浏览到 WDK 的安装文件夹，然后打开子目录工具，然后打开子目录 devcon，然后打开您的计算机的处理器体系结构匹配的子目录，，然后选择 Devcon.exe。 Devcon.exe 仅一次单击，然后执行尚不支持按**打开**。
    2.  中**自变量**文字框中，输入以下文本，其中*INFFile*是你的设备安装的信息 (INF) 文件的文件名和*HardwareID*是设备的硬件 ID:

        ```text
        update INFFile HardwareID 
        ```

    3.  在中**开始目录**文字框中，输入你的设备安装包的路径。
    4.  单击“打开” 。

6.  调试过程将开始，并 DevCon 安装您的驱动程序之前，WinDbg 将进入此 DevCon 进程。

7.  配置调试器在加载时中断到共同安装程序进程。 可以通过以下方法之一执行此操作：
    -   在调试器命令窗口中，使用[ **sxe （设置异常）** ](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)命令并后接**ld:** 以及然后共同安装程序中，不包括文件扩展名的文件名。 应该有没有空格的冒号后为例，如果辅助安装程序的名称是 mycoinst.dll，可以使用以下命令：
        ```dbgcmd
        sxe ld:mycoinst 
        ```

    -   选择**事件筛选器**WinDbg 的从**调试**菜单。 在中**事件筛选器**对话框中，选择**负载模块**。 下**执行**，选择**已启用。** 下**继续**，选择**未处理。** 单击**自变量**按钮，然后再在文本框中输入的共同安装程序中，不包括文件扩展名的文件名 （例如，对于 mycoinst.dll 输入"mycoinst"）。 单击**确定**，然后单击**关闭**。

8.  通过按 F5，或输入继续执行**g （转向）** 命令在调试器命令窗口中。

9.  加载辅助安装程序时，将返回到调试器中断执行。 此时，您可以设置所需的任何其他断点。

### <a name="span-idlimitationsofthisprocedurespanspan-idlimitationsofthisprocedurespanlimitations-of-this-procedure"></a><span id="limitations_of_this_procedure"></span><span id="LIMITATIONS_OF_THIS_PROCEDURE"></span>此过程的限制

在某些情况下，运行 DevCon 下的设备安装包可能会导致略有不同行为比的即插即用安装，由于不同的安全令牌和类似的内容。 如果想要调试共同安装程序中的特定问题，就可以，如果涉及到 DevCon，此问题将不会复制。 因此，然后再使用此方法，应使用 DevCon 没有调试程序附加到验证即插即用和 DevCon 方案中存在此问题的情况下安装的驱动程序。

如果问题消失 DevCon 启动安装时，你将需要调试而无需使用 DevCon 共同安装程序。 这是为了使用这样做的一种方法[TList](tlist.md)工具用于 **/m**选项，以确定哪个进程是共同安装程序模块加载，然后将调试器附加到该进程。

 

 






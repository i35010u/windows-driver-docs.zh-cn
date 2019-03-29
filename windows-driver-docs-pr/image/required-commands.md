---
title: 必需命令
description: 必需命令
ms.assetid: e4a82cc6-8031-4d67-bef8-1d73e2d98b6b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63b90d3206ffd0764e5abf8ebfa1c3ce3d2cb615
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569365"
---
# <a name="required-commands"></a>必需命令


## <span id="ddk_required_commands_si"></span><span id="DDK_REQUIRED_COMMANDS_SI"></span>


每个 microdriver 必须实现以下所需的命令集。

<span id="CMD_GETCAPABILITIES"></span><span id="cmd_getcapabilities"></span>CMD\_GETCAPABILITIES  
要获取按钮的事件信息的 WIA 平板驱动程序由调用。 传递的三个成员[ **VAL** ](https://msdn.microsoft.com/library/windows/hardware/ff548627)结构应填写： **lVal**应设置为的按钮; 的数目**pGuid**应设置为事件的 Guid; 的数组**ppButtonNames**可以选择性地设置**WCHAR** \*数组，其中包含的按钮中相同的顺序与它们的名称**pGuid** （适用于示例中，"扫描按钮"或"传真 Button"）。 如果**ppButtonNames**设置为**NULL**，WIA 平板驱动程序将创建泛型按钮名称。 数组可以分配以响应 CMD\_初始化和释放 cmd\_UNINITIALIZE。

<span id="CMD_INITIALIZE"></span><span id="cmd_initialize"></span>CMD\_初始化  
调用 WIA 平板驱动程序初始化 microdriver 并将设备 I/O 句柄设置为有效的值。 WIA 服务调用方法时此命令将发送到 microdriver [ **IWiaMiniDrv::drvInitializeWia** ](https://msdn.microsoft.com/library/windows/hardware/ff544986) WIA 平板驱动程序。

WIA 平板驱动程序将自动创建一个设备 I/O 句柄并将其放入**DeviceIOHandles**传递的数组成员[ **SCANINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff547361)位于索引 0 处的结构。 Microdriver 需要与设备通信时应使用此句柄。 如果 microdriver 需要其他设备 （例如，若要使用多个大容量 USB 管道） 的句柄，他们可以创建并存储在**DeviceIOHandles**最大数量的最大数组\_IO\_句柄。 WIA 平板驱动程序会自动关闭句柄位于索引 0，因为它在初始化期间创建该句柄。 其他句柄必须由响应 CMD microdriver 关闭\_UNINITIALIZE。

作为此命令的一部分，microdriver 应还初始化中的值的所有[ **SCANINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff547361)结构。 应设置 microdriver **SupportedDataTypes**， **IntensityRange**， **ContrastRange**， **BedWidth**，和**BedHeight** SCANINFO 的成员结构，以便 WIA 平板驱动程序可以自动验证这些值与设备的合法范围。

<span id="CMD_RESETSCANNER"></span><span id="cmd_resetscanner"></span>CMD\_RESETSCANNER  
调用 WIA 平板驱动程序的 WIA 服务请求的响应中将设备重置。 Microdriver 应设置为开启状态的设备。 在 Windows Vista 中，WIA 平板驱动程序不使用此命令。 但是，microdrivers 应继续支持此命令，以确保正确操作在 Windows XP 中，并且可能在将来可能会使用此命令的 WIA 平板驱动程序版本。

<span id="CMD_SETDATATYPE"></span><span id="cmd_setdatatype"></span>CMD\_SETDATATYPE  
由要扫描的数据类型设置的 WIA 平板驱动程序调用。 传递以下值之一**lVal**成员传递[ **VAL** ](https://msdn.microsoft.com/library/windows/hardware/ff548627)结构：

WIA\_数据\_阈值 − 1 位黑色/白色

WIA\_数据\_灰度 − 8 位灰度

WIA\_数据\_颜色 − 24 位颜色

Microdriver 应存储中的值**数据类型**成员传递[ **SCANINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff547361)结构。

<span id="CMD_SETCONTRAST"></span><span id="cmd_setcontrast"></span>CMD\_SETCONTRAST  
调用 WIA 平板驱动程序将扫描的对比度值。 所需的对比度值传入**lVal**成员传递[ **VAL** ](https://msdn.microsoft.com/library/windows/hardware/ff548627)结构。 值 −1000 应解释为最小对比度值，0 名义，到 1000年设备的最大对比度。 Microdriver 应存储中的值**对比度**成员传递[ **SCANINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff547361)结构。

<span id="CMD_SETINTENSITY"></span><span id="cmd_setintensity"></span>CMD\_SETINTENSITY  
调用 WIA 平板驱动程序设置的强度或扫描的亮度值。 所需的强度值传入**lVal**成员传递[ **VAL** ](https://msdn.microsoft.com/library/windows/hardware/ff548627)结构。 值 −1000 应解释为最低的亮度值为 0 名义，到 1000年设备的最大亮度。 Microdriver 应存储中的值**强度**成员传递[ **SCANINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff547361)结构。

<span id="CMD_SETXRESOLUTION"></span><span id="cmd_setxresolution"></span>CMD\_SETXRESOLUTION  
由 WIA 平板驱动程序设置水平扫描解析调用。 以像素为单位的所需的分辨率传入**lVal**成员传递[ **VAL** ](https://msdn.microsoft.com/library/windows/hardware/ff548627)结构。 Microdriver 应存储中的值**XResolution**成员传递[ **SCANINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff547361)结构。

<span id="CMD_SETYRESOLUTION"></span><span id="cmd_setyresolution"></span>CMD\_SETYRESOLUTION  
由 WIA 平板驱动程序设置垂直扫描解析调用。 以像素为单位的所需的分辨率传入**lVal**传递 VAL 结构中的成员。 Microdriver 应存储中的值**YResolution**传递 SCANINFO 结构中的成员。

<span id="CMD_STI_DEVICERESET"></span><span id="cmd_sti_devicereset"></span>CMD\_STI\_DEVICERESET  
调用 WIA 平板驱动程序以响应仍映像 (STI) 请求将设备重置。 在初始化过程中通常只有一次调用此命令。

<span id="CMD_STI_DIAGNOSTIC"></span><span id="cmd_sti_diagnostic"></span>CMD\_STI\_诊断  
当用户请求设备的测试时，由 WIA 平板驱动程序调用。

<span id="CMD_UNINITIALIZE"></span><span id="cmd_uninitialize"></span>CMD\_UNINITIALIZE  
取消初始化 microdriver 和关闭设备 I/O 句柄。 WIA 平板驱动程序会自动关闭设备 I/O 句柄**DeviceIOHandles**的数组成员[ **SCANINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff547361)结构，位于索引 0 处。 此命令将发送到 microdriver 时卸载 WIA 平板驱动程序。

 

 






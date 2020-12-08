---
title: 必需命令
description: 必需命令
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd03674475bdf31d537045e535ac7b03f11799d8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817327"
---
# <a name="required-commands"></a>必需命令


## <span id="ddk_required_commands_si"></span><span id="DDK_REQUIRED_COMMANDS_SI"></span>


以下必需命令集必须由每个 microdriver 实现。

<span id="CMD_GETCAPABILITIES"></span><span id="cmd_getcapabilities"></span>CMD \_ GETCAPABILITIES  
由 WIA 平板驱动程序调用以获取按钮事件信息。 应填写传递的 [**VAL**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)结构的三个成员：应将 **lVal** 设置为按钮数;应将 **pGuid** 设置为事件 guid 的数组;可以选择将 **ppButtonNames** 设置为 **WCHAR** \* 包含按钮名称的 WCHAR 数组，其顺序与 **PGuid** (例如，"扫描按钮" 或 "传真按钮" ) 相同。 如果 **ppButtonNames** 设置为 **NULL**，WIA 平板驱动程序将创建通用按钮名称。 可以分配数组以响应 CMD \_ INITIALIZE，并在 cmd 取消初始化中释放 \_ 。

<span id="CMD_INITIALIZE"></span><span id="cmd_initialize"></span>CMD \_ 初始化  
由 WIA 平板驱动程序调用以初始化 microdriver，并将设备 i/o 句柄设置为有效值。 当 WIA 服务在 WIA 平板驱动程序上调用方法 [**IWiaMiniDrv：:D rvinitializewia**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia) 时，此命令将发送到 microdriver。

WIA 平板驱动程序将自动创建一个设备 i/o 句柄，并将其放在索引0处传递的 [**SCANINFO**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-_scaninfo)结构的 **DeviceIOHandles** 数组成员中。 当 microdriver 需要与设备通信时，应使用此句柄。 例如，如果 microdriver 需要其他设备句柄 (例如，若要使用多个批量 USB 管道) ，可以在 **DeviceIOHandles** 数组中创建并存储它们，直到达到最大 \_ IO 句柄的最大数量 \_ 。 WIA 平板驱动程序将自动关闭索引0处的句柄，因为该句柄是在初始化过程中创建的。 其他句柄必须由 microdriver 关闭以响应 CMD 取消 \_ 初始化。

作为此命令的一部分，microdriver 还应初始化 [**SCANINFO**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-_scaninfo) 结构中的所有值。 Microdriver 应设置 BEDWIDTH 结构的 **SupportedDataTypes**、 **IntensityRange**、 **ContrastRange**、 **BedHeight** 和 **SCANINFO** 成员，以便 WIA 平板驱动程序可以根据设备的合法范围自动验证这些值。

<span id="CMD_RESETSCANNER"></span><span id="cmd_resetscanner"></span>CMD \_ RESETSCANNER  
由 WIA 平板驱动程序调用以重置设备，以响应 WIA 服务请求。 Microdriver 应将设备设置为其开机状态。 在 Windows Vista 中，WIA 平板驱动程序不使用此命令。 但是，microdrivers 应继续支持此命令，以确保在 Windows XP 中以及可能使用此命令的未来版本的 WIA 平板驱动程序中正确操作。

<span id="CMD_SETDATATYPE"></span><span id="cmd_setdatatype"></span>CMD \_ SETDATATYPE  
由 WIA 平板驱动程序调用以设置扫描的数据类型。 在传递的 [**VAL**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)结构的 **lVal** 成员中传递以下值之一：

WIA \_ 数据 \_ 阈值−1位黑色/白色

WIA \_ 数据 \_ 灰度−8位灰度

WIA \_ 数据 \_ 颜色−24位颜色

Microdriver 应将值存储在传递的 [**SCANINFO**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-_scaninfo)结构的 **数据类型** 成员中。

<span id="CMD_SETCONTRAST"></span><span id="cmd_setcontrast"></span>CMD \_ SETCONTRAST  
由 WIA 平板驱动程序调用以设置扫描的对比度值。 所需对比度值将传递到传递的 [**VAL**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)结构的 **lVal** 成员中。 应将值−1000解释为最小对比度值（0），并将设备的最大对比度解释为1000。 Microdriver 应将值存储在传递的 [**SCANINFO**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-_scaninfo)结构的 **对比度** 成员中。

<span id="CMD_SETINTENSITY"></span><span id="cmd_setintensity"></span>CMD \_ SETINTENSITY  
由 WIA 平板驱动程序调用以设置扫描的强度或亮度值。 所需的强度值将传递到传递的 [**VAL**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)结构的 **lVal** 成员中。 应将值−1000解释为最小亮度值，0公称，并将设备的最大亮度解释为1000。 Microdriver 应将值存储在传递的 [**SCANINFO**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-_scaninfo)结构的 **强度** 成员中。

<span id="CMD_SETXRESOLUTION"></span><span id="cmd_setxresolution"></span>CMD \_ SETXRESOLUTION  
由 WIA 平板驱动程序调用以设置水平扫描分辨率。 所需的分辨率（以像素为单位）传递到传递的 [**VAL**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)结构的 **lVal** 成员中。 Microdriver 应将值存储在传递的 [**SCANINFO**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-_scaninfo)结构的 **XResolution** 成员中。

<span id="CMD_SETYRESOLUTION"></span><span id="cmd_setyresolution"></span>CMD \_ SETYRESOLUTION  
由 WIA 平板驱动程序调用以设置垂直扫描分辨率。 所需的分辨率（以像素为单位）传递到传递的 VAL 结构的 **lVal** 成员中。 Microdriver 应将值存储在传递的 SCANINFO 结构的 **YResolution** 成员中。

<span id="CMD_STI_DEVICERESET"></span><span id="cmd_sti_devicereset"></span>CMD \_ STI \_ DEVICERESET  
WIA 平板驱动程序调用以重置设备，以响应静态图像 (STI) 请求。 在初始化期间，通常只调用一次此命令。

<span id="CMD_STI_DIAGNOSTIC"></span><span id="cmd_sti_diagnostic"></span>CMD \_ STI \_ 诊断  
当用户请求设备测试时，WIA 平板驱动程序调用。

<span id="CMD_UNINITIALIZE"></span><span id="cmd_uninitialize"></span>CMD 取消 \_ 初始化  
取消初始化 microdriver 并关闭设备 i/o 句柄。 WIA 平板驱动程序将自动关闭 [**SCANINFO**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-_scaninfo)结构的 **DeviceIOHandles** 数组成员中索引0处的设备 i/o 句柄。 当 WIA 平板驱动程序卸载时，此命令将发送到 microdriver。

 


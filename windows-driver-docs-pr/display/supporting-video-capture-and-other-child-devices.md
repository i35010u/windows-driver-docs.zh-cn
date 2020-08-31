---
title: 支持视频捕获和其他子设备
description: 支持视频捕获和其他子设备
ms.assetid: 15575700-7525-459e-a099-158f0c13899c
keywords:
- 视频捕获 WDK 显示
- 捕获视频 WDK 显示
- 接口 WDK 显示
- 子视频捕获驱动程序 WDK 显示
- MDLs WDK 显示
- 内存描述符列出了 WDK 显示
- 捕获缓冲区 WDK 显示
- 显示驱动程序模型 WDK Windows Vista，子视频捕获驱动程序
- Windows Vista 显示器驱动程序模型 WDK，子视频捕获驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfb7c1211a46e0bad9557450f40f9c4a7902e84f
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063792"
---
# <a name="supporting-video-capture-and-other-child-devices"></a>支持视频捕获和其他子设备


视频捕获设备或其他子设备的显示微型端口驱动程序和驱动程序可以相互定义专用接口，子驱动程序可以使用该接口通过父微型端口驱动程序与其设备通信。 子视频捕获驱动程序必须紧耦合到父显示器微型端口驱动程序。 事实上，视频捕获可能作为显示微型端口驱动程序的一部分实现。 视频捕获驱动程序可以将专用接口与显示微型端口驱动程序一起使用，以访问 *I2C* 总线和其他目的。

为了初始化专用接口，视频捕获驱动程序会将 [**IRP \_ MN \_ 查询 \_ 接口**](../kernel/irp-mn-query-interface.md) 请求发送到显示端口驱动程序 (显示微型端口驱动程序 *Dxgkrnl.sys*) 的一部分。 在显示端口驱动程序收到此类请求后，它将调用微型端口驱动程序的 [**DxgkDdiQueryInterface**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface) 函数，并传递指向 [**查询 \_ 接口**](/windows-hardware/drivers/ddi/video/ns-video-_query_interface) 结构的指针，该结构包含用于初始化专用接口的信息。

**注意**   如果视频捕获是作为显示微型端口驱动程序的一部分实现的，则视频捕获可能会直接调用*DxgkDdiQueryInterface* 。

 

 (包括视频捕获设备) 子设备的每个驱动程序都必须返回指示与设备关联的硬件的适配器 GUID。 适配器 GUID 提供给[**DXGK \_ 启动 \_ 信息**](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_start_info)结构的**AdapterGuid**成员中的显示微型端口驱动程序，该驱动程序由在初始化适配器时发送的[**DxgkDdiStartDevice**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device)函数的*DxgkStartInfo*参数指向。 用户模式捕获组件随后可以将此适配器 GUID 映射到显示适配器。

在 Microsoft Windows 2000 中，显示驱动程序模型结构并将 MDLs 发送到视频捕获驱动程序。 除了支持捕获到系统内存之外，Windows Vista 显示器驱动程序模型还支持捕获到视频内存。 Direct3D 运行时调用 DirectX 视频加速2.0 类型的函数，以指示 GPU 对捕获数据执行 post 处理。 用户模式显示驱动程序将发送 D3DKMT 的 \_ 句柄类型值来捕获缓冲区分配，而不是发送 MDLs 来描述视频内存缓冲区。 因此，视频捕获驱动程序和显示微型端口驱动程序组合可以使用现有的回调函数（如 [**DxgkCbGetHandleData**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_gethandledata) ）来引用描述捕获缓冲区的专用数据。 驱动程序组合还可以使用 [**DxgkCbGetCaptureAddress**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_getcaptureaddress) 回调函数返回捕获缓冲区的物理地址。

视频捕获应用程序调入到 Direct3D 运行时以创建捕获缓冲区;运行时随后调用用户模式显示驱动程序。 运行时调用用户模式显示驱动程序的[**CreateResource**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数，并在[**D3DDDIARG \_ CreateResource**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构的**Flags**成员中设置**CaptureBuffer**位字段标志来创建捕获缓冲区。 当内存管理器调用显示小型端口驱动程序的[**DxgkDdiCreateAllocation**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)函数来为捕获缓冲区创建分配时，显示微型端口驱动程序还必须为视频内存管理器指定**捕获**位字段标志。 创建捕获缓冲区后，它们会立即固定在内存中，并且在释放之前不会进行取消固定。 因为捕获堆栈必须将捕获缓冲区的内核模式分配句柄发送到捕获驱动程序，所以运行时将调用用户模式显示驱动程序的 [**GetCaptureAllocationHandle**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaptureallocationhandle) 函数，以将每个资源句柄映射到该资源的内核模式分配句柄。

捕获驱动程序可以报告它是否支持直接捕获到系统内存。 如果捕获驱动程序支持直接捕获到系统内存，则会将 MDLs 发送到捕获驱动程序以实现此目的。 如果捕获驱动程序不支持直接捕获到系统内存，则运行时将创建视频内存捕获缓冲区，并且捕获驱动程序必须填写它们。 调用用户模式显示驱动程序的 [**CaptureToSysMem**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_capturetosysmem) 函数将捕获缓冲区的内容复制到系统内存图面。 运行时可以使用 *CaptureToSysMem* 而不是 [**Blt**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_blt) 函数来利用特殊硬件进行位块传输 (bitblt) ，而不要求用户模式显示驱动程序调用 [**pfnRenderCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb) 函数。

由于 AVStream 控制视频捕获，因此在发生视频捕获时，DirectX 图形内核子系统并不知道。 但是，图形内核子系统知道用作捕获缓冲区的分配。 当捕获缓冲区即将被销毁时，图形内核子系统将调用显示微型端口驱动程序的 [**DxgkDdiStopCapture**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_stopcapture) 函数，以指示捕获操作必须立即停止使用分配作为捕获缓冲区。 如果捕获操作已通过捕获堆栈停止，则驱动程序可以放心地忽略调用。

 


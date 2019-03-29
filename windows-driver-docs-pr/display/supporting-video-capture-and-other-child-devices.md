---
title: 支持视频捕获和其他子设备
description: 支持视频捕获和其他子设备
ms.assetid: 15575700-7525-459e-a099-158f0c13899c
keywords:
- 视频捕获 WDK 显示
- 捕获视频 WDK 显示
- 接口 WDK 显示
- 显示子视频捕获驱动程序 WDK
- MDLs WDK 显示
- 内存描述符列出 WDK 显示
- 捕获的缓冲区 WDK 显示
- 显示驱动程序模型 WDK Windows Vista 中，子视频捕获驱动程序
- Windows Vista 显示器驱动程序模型 WDK，子视频捕获驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a43286d0ba1afe731a2abd58a4271ec60671450
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565245"
---
# <a name="supporting-video-capture-and-other-child-devices"></a>支持视频捕获和其他子设备


显示微型端口驱动程序和视频捕获设备或另一个子设备驱动程序可以相互定义子驱动程序可以使用与父微型端口驱动程序通过其设备进行通信的专用接口。 子视频捕获驱动程序必须紧密耦合到父显示微型端口驱动程序。 实际上，可能无法显示微型端口驱动程序的一部分实现视频捕获。 视频捕获驱动程序可以使用专用接口通过显示微型端口驱动程序访问*I2C*总线和出于其他目的。

若要初始化的专用接口，视频捕获驱动程序将发送[ **IRP\_MN\_查询\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff551687)显示端口驱动程序 （的一部分的请求*Dxgkrnl.sys*) 显示微型端口驱动程序。 显示端口驱动程序将收到此类请求后，它会调用微型端口驱动程序[ **DxgkDdiQueryInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff559764)函数，并将传递一个指向[**查询\_界面**](https://msdn.microsoft.com/library/windows/hardware/ff569225)结构，其中包含要初始化的专用接口的信息。

**请注意**  如果显示微型端口驱动程序的一部分实施视频捕获，则可能会调用视频捕获*DxgkDdiQueryInterface*直接。

 

子设备 （包括视频捕获设备） 的每个驱动程序必须返回适配器指示设备是与相关联的硬件的 GUID。 GUID 提供为显示微型端口驱动程序中的适配器**AdapterGuid**的成员[ **DXGK\_启动\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff562055)结构通过指向*DxgkStartInfo*的参数[ **DxgkDdiStartDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff560775)时初始化适配器发送的函数。 用户模式下捕获组件随后可以将此适配器 GUID 映射到显示适配器。

在 Microsoft Windows 2000 显示器驱动程序模型结构和发送到视频 MDLs 捕获驱动程序。 除了支持捕获到系统内存，Windows Vista 显示器驱动程序模型支持捕获视频内存。 Direct3D 运行时调用 DirectX 视频加速 2.0 类型函数，以直接 GPU 执行后期处理捕获的数据。 而不是发送 MDLs 来描述视频内存缓冲区，用户模式显示驱动程序将发送 D3DKMT\_句柄，以捕获缓冲区分配的句柄类型值。 因此，视频捕获驱动程序和显示微型端口驱动程序组合可以使用现有的回调函数，如[ **DxgkCbGetHandleData** ](https://msdn.microsoft.com/library/windows/hardware/ff559515)引用描述捕获的专用数据缓冲区。 此外可以使用驱动程序组合[ **DxgkCbGetCaptureAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff559510)回调函数以返回在捕获缓冲区的物理地址。

视频捕获应用程序调用 Direct3D 运行时创建捕获缓冲区;用户模式显示驱动程序会随后调用运行时。 运行时调用用户模式显示驱动程序[ **CreateResource** ](https://msdn.microsoft.com/library/windows/hardware/ff540688)函数与**CaptureBuffer**中设置位域标志**标志**的成员[ **D3DDDIARG\_CREATERESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff542963)结构，以创建捕获缓冲区。 显示微型端口驱动程序还必须指定**捕获**视频内存管理器时内存管理器调用显示微型端口驱动程序的位域标志[ **DxgkDdiCreateAllocation**](https://msdn.microsoft.com/library/windows/hardware/ff559606)函数来创建用于捕获缓冲区的分配。 当创建捕获缓冲区时，这些立即固定在内存中，直到它们被释放不解除固定。 运行时捕获堆栈必须捕获驱动程序，用于捕获缓冲区发送内核模式分配句柄，因为调用用户模式显示驱动程序[ **GetCaptureAllocationHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff566771)若要将每个资源句柄映射到该资源的内核模式分配句柄的函数。

捕获驱动程序可以报告它是否支持直接捕获到系统内存。 如果捕获驱动程序支持捕获直接到系统内存，MDLs 发送到捕获驱动程序实现此目的。 如果捕获驱动程序不支持直接捕获到系统内存，运行时创建视频内存捕获缓冲区，并捕获驱动程序必须填充它们。 用户模式显示驱动程序[ **CaptureToSysMem** ](https://msdn.microsoft.com/library/windows/hardware/ff539363)函数调用以将捕获缓冲区的内容复制到系统内存图面。 可以使用运行时*CaptureToSysMem*而不是[ **Blt** ](https://msdn.microsoft.com/library/windows/hardware/ff538251)函数以利用的位块传输 (bitblt) 的不需要的特殊硬件用户模式显示驱动程序调用[ **pfnRenderCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568923)函数。

因为 AVStream 控制视频捕获，并不知道视频捕获发生时的 DirectX 图形内核子系统。 但是，图形内核子系统可察觉用作捕获缓冲区的分配。 图形内核子系统时捕获缓冲区即将被销毁，调用显示微型端口驱动程序[ **DxgkDdiStopCapture** ](https://msdn.microsoft.com/library/windows/hardware/ff560776)函数来指示捕获操作必须立即停止将用作在捕获缓冲区的分配。 如果已通过捕获堆栈停止捕获操作，该驱动程序可以放心地忽略该调用。

 

 






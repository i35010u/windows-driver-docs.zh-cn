---
title: 多平面覆盖 VidPN 呈现
ms.assetid: BAD7FD48-905D-4547-8C69-133240B39FA3
description: 适用于使用在多个图面上显示的函数的要求。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ea8a5bd67758f98cd2c0337b58613a84201dc59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345597"
---
# <a name="multiplane-overlay-vidpn-presentation"></a>多平面覆盖 VidPN 呈现


当使用 multiplane 叠加时，这些要求适用于用于视频存在网络 (VidPNs) 中的多个面上呈现的函数：

<span id="DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay"></span><span id="dxgkddisetvidpnsourceaddresswithmultiplaneoverlay"></span><span id="DXGKDDISETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY"></span>[*DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay*](https://msdn.microsoft.com/library/windows/hardware/hh780298)  
-   如果[ **DXGK\_MULTIPLANE\_覆盖\_平面**](https://msdn.microsoft.com/library/windows/hardware/hh780305)。**启用**为 false，显示微型端口驱动程序应禁用指定的平面。
-   如果在上一个调用中启用了一个平面[ *DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay* ](https://msdn.microsoft.com/library/windows/hardware/hh780298)但在当前调用中不存在，该驱动程序应继续显示而无需平面翻转它。
-   很可能该驱动程序将接收到多个调用[ *DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay* ](https://msdn.microsoft.com/library/windows/hardware/hh780298)相同垂直同步期间 (一次调用翻转一个平面和另一个调用翻转另一个平面）。 在这种情况下，该驱动程序应处理两次调用。
-   应在受信任的来源的用户模式下验证传递的数据。 但是，显示微型端口驱动程序仍应检查以确保它不会导致问题的数据。 如果数据不正确，该驱动程序可能会失败与调用**状态\_无效\_参数**错误代码，但此类故障可能不正常处理和表示任一 bug 在操作系统中或在用户模式驱动程序。

<span id="DxgkDdiSetVidPnSourceVisibility"></span><span id="dxgkddisetvidpnsourcevisibility"></span><span id="DXGKDDISETVIDPNSOURCEVISIBILITY"></span>[*DxgkDdiSetVidPnSourceVisibility*](https://msdn.microsoft.com/library/windows/hardware/ff560771)  
当[ **DXGKARG\_SETVIDPNSOURCEVISIBILITY**](https://msdn.microsoft.com/library/windows/hardware/ff559486)。**可见**设置为**FALSE**上对此函数的调用中的给定源，所有硬件平面必须都禁用，包括用于主表面的层。 当**Visible**设置为**TRUE**，必须启用用于主表面平面，并且所有其他平面必须保持禁用状态。

<span id="DxgkDdiSetVidPnSourceAddress"></span><span id="dxgkddisetvidpnsourceaddress"></span><span id="DXGKDDISETVIDPNSOURCEADDRESS"></span>[*DxgkDdiSetVidPnSourceAddress*](https://msdn.microsoft.com/library/windows/hardware/ff560767)  
当调用此函数时，该驱动程序应禁用所有非主覆盖平面。 使用翻转主表面[ *DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay* ](https://msdn.microsoft.com/library/windows/hardware/hh780298)处于 multiplane 覆盖模式时。

 

 






---
title: 支持 GetDriverInfo2
description: 支持 GetDriverInfo2
ms.assetid: 5e2dd363-9e72-4674-940e-8b4f06f6eb14
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，GetDriverInfo2
- GetDriverInfo2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7aa383699431b8a625772de198ffef7d94325ee1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825623"
---
# <a name="supporting-getdriverinfo2"></a>支持 GetDriverInfo2


## <span id="ddk_supporting_getdriverinfo2_gg"></span><span id="DDK_SUPPORTING_GETDRIVERINFO2_GG"></span>


DirectX 8.0 DDI 引入了一种新的机制，用于查询驱动程序的信息。 此机制扩展现有的[**DdGetDriverInfo**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)入口点，以查询来自驱动程序的其他信息。 目前，此机制仅用于查询 DX8 样式 D3D cap。

**请   注意**，在阅读下面的 GetDriverInfo2 时，可能会问到为什么需要机制。 只需定义一个新的**GetDriverInfo** GUID，驱动程序就会通过返回 D3DCAP8 结构来处理该 GUID。 以下各段中引入的**GetDriverInfo2**是一种机制，用于最大程度地减少对 Windows 操作系统所需的更改，以启用 directx 8.0 级别功能，从而使 directx 8.0 运行时切实可行。

 

此扩展到**GetDriverInfo**采用 GUID\_GetDriverInfo2 形式的*DdGetDriverInfo*调用。 当驱动程序收到具有该 GUID 的*DdGetDriverInfo*调用时，它必须检查在[**DD\_GETDRIVERINFODATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)数据结构的**lpvData**字段中传递的数据结构，以查看所请求的信息。 如下所述， **lpvData**可以指向[**dd\_GETDRIVERINFO2DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getdriverinfo2data)或[**dd\_STEREOMODE**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_stereomode)结构。

GUID\_GetDriverInfo2 的 guid 值与 GUID\_DDStereoMode 相同。 如果驱动程序未处理 GUID\_DDStereoMode，则不会出现问题。 但是，如果你的 DirectX 8.0 驱动程序处理 GUID\_DDStereoMode，请注意，当使用 GUID\_GetDriverInfo2 （GUID\_DDStereoMode）调用*DdGetDriverInfo*时，运行时将 DD\_dwHeight 结构的**STEREOMODE**字段设置为特殊值 D3DGDI2\_幻数。 此字段对应于 DD\_GETDRIVERINFO2DATA 结构的**dwMagic**字段。 因此，通过将**lpvData**指针转换为指向 DD\_STEREOMODE 结构的指针或指向 DD\_GETDRIVERINFO2DATA 结构的指针，并检查值 DWMAGIC\_幻的相应字段（**dwHeight**或**D3DGDI2**）的值，你可以区分调用来确定立体声模式功能或请求 Direct3D 8.0 功能。

一旦驱动程序确定这是对**GetDriverInfo2**的调用，就必须确定运行时请求的信息类型。 此类型包含在 DD\_GETDRIVERINFO2DATA 数据结构的**dwType**字段中。

最后，驱动程序将请求的数据复制到提供的缓冲区中。 需要注意的一点是，DD\_GETDRIVERINFODATA 的**lpvData**字段指向要将请求的数据复制到的缓冲区。 **lpvData**还指向 DD\_GETDRIVERINFO2DATA 结构。 这意味着，驱动程序返回的数据将覆盖 DD\_GETDRIVERINFO2DATA 结构（因此，DD\_GETDRIVERINFO2DATA 结构占据缓冲区的前几个 Dword）。

若要使用**GetDriverInfo2**进行调用并报告 DirectX 8.0 功能，驱动程序必须在由驱动程序返回的[**DD\_HALINFO**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)结构的**dwFlags**字段中设置新的标志 DDHALINFO\_GetDriverInfo2。 如果未设置此标志，则运行时不会将**GetDriverInfo2**调用发送给驱动程序，并且不会将驱动程序识别为 DirectX 8.0 级别驱动程序。

运行时使用类型为 D3DGDI2 的**GetDriverInfo2**\_类型\_DXVERSION 通知应用程序正在使用的当前 DX 运行时版本的驱动程序。 运行时在 DD\_GETDRIVERINFODATA 的**lpvData**字段中提供了一个指向[**dd\_DXVERSION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_dxversion)结构的指针。

 

 






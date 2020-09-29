---
title: 支持 GetDriverInfo2
description: 支持 GetDriverInfo2
ms.assetid: 5e2dd363-9e72-4674-940e-8b4f06f6eb14
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，GetDriverInfo2
- GetDriverInfo2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f48dca22563c757c9622fc1afc1e507fa46d9a59
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91424034"
---
# <a name="supporting-getdriverinfo2"></a>支持 GetDriverInfo2


## <span id="ddk_supporting_getdriverinfo2_gg"></span><span id="DDK_SUPPORTING_GETDRIVERINFO2_GG"></span>


DirectX 8.0 DDI 引入了一种新的机制，用于查询驱动程序的信息。 此机制扩展现有的 [**DdGetDriverInfo**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverinfo) 入口点，以查询来自驱动程序的其他信息。 目前，此机制仅用于查询 DX8 样式 D3D cap。

**注意**   阅读以下各项后，可能会提出**GetDriverInfo2**机制必不可少的问题。 只需定义一个新的 **GetDriverInfo** GUID，驱动程序就会通过返回 D3DCAP8 结构来处理该 GUID。 以下各段中引入的**GetDriverInfo2**是一种机制，用于最大程度地减少对 Windows 操作系统所需的更改，以启用 directx 8.0 级别功能，从而使 directx 8.0 运行时切实可行。

 

此扩展到 **GetDriverInfo** 采用 GUID GetDriverInfo2 形式的 *DdGetDriverInfo* 调用 \_ 。 当驱动程序收到具有该 GUID 的*DdGetDriverInfo*调用时，它必须检查在[**DD \_ GETDRIVERINFODATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_getdriverinfodata)数据结构的**lpvData**字段中传递的数据结构，以查看所请求的信息。 如下所述， **lpvData** 可以指向 [**Dd \_ GETDRIVERINFO2DATA**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getdriverinfo2data) 或 [**dd \_ STEREOMODE**](/windows/win32/api/ddrawint/ns-ddrawint-dd_stereomode) 结构。

GUID \_ GetDriverInfo2 与 guid DDStereoMode 具有相同的 guid 值 \_ 。 如果驱动程序未处理 GUID \_ DDStereoMode，则不会出现问题。 但是，如果您的 DirectX 8.0 驱动程序处理 GUID \_ DDStereoMode，请注意，当*DdGetDriverInfo*调用具有 GUID \_ GetDriverInfo2 (Guid DDStereoMode) 的 DdGetDriverInfo 时 \_ ，运行时会将 DD dwHeight 结构的**STEREOMODE**字段设置 \_ 为特殊值 D3DGDI2 幻数 \_ 。 此字段对应于 DD GETDRIVERINFO2DATA 结构的 **dwMagic** 字段 \_ 。 因此，通过将 **lpvData** 指针转换为指向 dd STEREOMODE 结构的指针 \_ 或指向 dd \_ GETDRIVERINFO2DATA 结构的指针，并检查相应字段 (**dwHeight** 或 **dwMagic**) 对于值 D3DGDI2 幻数的值 \_ ，可以区分调用来确定立体声模式功能或 Direct3D 8.0 功能的请求。

一旦驱动程序确定这是对 **GetDriverInfo2** 的调用，就必须确定运行时请求的信息类型。 此类型包含在 DD GETDRIVERINFO2DATA 数据结构的 **dwType** 字段中 \_ 。

最后，驱动程序将请求的数据复制到提供的缓冲区中。 请务必注意，DD GETDRIVERINFODATA 数据结构的 **lpvData** 字段 \_ 指向要将请求的数据复制到的缓冲区。 **lpvData** 也指向 DD \_ GETDRIVERINFO2DATA 结构。 这意味着，驱动程序返回的数据将覆盖 DD \_ GETDRIVERINFO2DATA 结构 (，因此，dd \_ GETDRIVERINFO2DATA 结构会占用缓冲区的前几个 dword) 。

若要使用**GetDriverInfo2**进行调用并报告 DirectX 8.0 功能，驱动程序必须 \_ 在由驱动程序返回的[**DD \_ HALINFO**](/windows/win32/api/ddrawint/ns-ddrawint-dd_halinfo)结构的**DWFLAGS**字段中设置新的标志 DDHALINFO GetDriverInfo2。 如果未设置此标志，则运行时不会将 **GetDriverInfo2** 调用发送给驱动程序，并且不会将驱动程序识别为 DirectX 8.0 级别驱动程序。

运行时使用类型为 D3DGDI2 的 **GetDriverInfo2** 的 \_ \_ DXVERSION 通知驱动程序正在使用的当前 DX 运行时版本的驱动程序。 运行时在 DD GETDRIVERINFODATA 的**lpvData**字段中提供了一个指向[**dd \_ DXVERSION**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_dxversion)结构的指针 \_ 。

 


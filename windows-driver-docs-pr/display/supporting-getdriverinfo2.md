---
title: 支持 GetDriverInfo2
description: 支持 GetDriverInfo2
ms.assetid: 5e2dd363-9e72-4674-940e-8b4f06f6eb14
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，GetDriverInfo2
- GetDriverInfo2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6549b1da3cc2c0d814e02fae247b8028de0816ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533485"
---
# <a name="supporting-getdriverinfo2"></a>支持 GetDriverInfo2


## <span id="ddk_supporting_getdriverinfo2_gg"></span><span id="DDK_SUPPORTING_GETDRIVERINFO2_GG"></span>


DirectX 8.0 DDI 引入了一种新机制用于查询的信息的驱动程序。 此机制扩展了现有[ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)驱动程序的入口点以查询有关其他信息。 目前，此机制仅用于实现查询 DX8 样式 D3D cap。

**请注意**  读取以下可能会问为什么**GetDriverInfo2**机制是有必要。 这看起来更可取的方法只需定义一个新**GetDriverInfo**驱动程序将处理通过返回 D3DCAP8 结构的 GUID。 **GetDriverInfo2**（在以下各段中引入) 是一种机制来最大程度减少到了 Windows 操作系统，系统以启用 DirectX 8.0 级别功能，从而可以重新分发 DirectX 8.0 运行时实际所需的更改。

 

此扩展**GetDriverInfo**采用的形式*DdGetDriverInfo*调用使用 GUID\_GetDriverInfo2。 当*DdGetDriverInfo*驱动程序接收到使用该 GUID 的调用，它必须检查传入的数据结构**lpvData**字段[ **DD\_GETDRIVERINFODATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551550)数据结构，以查看为其请求哪些信息。 如下所述**lpvData**可以是指向[ **DD\_GETDRIVERINFO2DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551548)或[ **DD\_STEREOMODE** ](https://msdn.microsoft.com/library/windows/hardware/ff551716)结构。

GUID\_GetDriverInfo2 是相同 GUID 的 GUID 值\_DDStereoMode。 如果您的驱动程序不会处理 GUID\_DDStereoMode，这不是一个问题。 但是，如果您的 DirectX 8.0 驱动程序处理 GUID\_DDStereoMode，请注意，当调用*DdGetDriverInfo*具有 GUID\_GetDriverInfo2 (GUID\_DDStereoMode) 进行时，运行时设置**dwHeight**字段的 DD\_STEREOMODE 结构为特殊值 D3DGDI2\_MAGIC。 此字段对应于**dwMagic** DD 字段\_GETDRIVERINFO2DATA 结构。 因此，通过强制转换**lpvData**指向 DD 指针\_STEREOMODE 结构或指向 DD\_GETDRIVERINFO2DATA 结构和检查相应的值字段 (**dwHeight**或**dwMagic**) 的值 D3DGDI2\_的神奇功能，你可以区分调用，以确定立体声模式功能或 Direct3D 8.0 功能的请求。

该驱动程序已确定这是对的调用后**GetDriverInfo2**它然后必须确定运行时所请求的信息的类型。 此类型包含在**dwType** DD 字段\_GETDRIVERINFO2DATA 数据结构。

最后，该驱动程序将请求的数据复制到所提供的缓冲区。 务必要注意**lpvData** DD 字段\_GETDRIVERINFODATA 数据结构指向要将所请求的数据复制到缓冲区。 **lpvData**还指向 DD\_GETDRIVERINFO2DATA 结构。 这意味着该驱动程序返回的数据将覆盖 DD\_GETDRIVERINFO2DATA 结构 (，因此，DD\_GETDRIVERINFO2DATA 结构占用的缓冲区的第几个 dword 值)。

若要使用调用**GetDriverInfo2**，和 DirectX 8.0 报表功能，它是所必需的驱动程序以设置新标志 DDHALINFO\_中的 GETDRIVERINFO2 **dwFlags**字段[ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)驱动程序返回的结构。 如果未设置此标志，在运行时不会发送**GetDriverInfo2**对驱动程序和驱动程序的调用未被识别为 DirectX 8.0 级别驱动程序。

运行时使用**GetDriverInfo2**与类型 D3DGDI2\_类型\_DXVERSION 以通知应用程序正在使用的当前 DX 运行时版本的驱动程序。 在运行时提供一个指针指向[ **DD\_DXVERSION** ](https://msdn.microsoft.com/library/windows/hardware/ff551515)结构**lpvData** DD 字段\_GETDRIVERINFODATA。

 

 






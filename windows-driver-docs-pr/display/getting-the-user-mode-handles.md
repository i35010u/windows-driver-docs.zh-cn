---
title: 获取用户模式句柄
description: 获取用户模式句柄
ms.assetid: b241bf00-1adb-4ab0-a00e-e922bdc9eee5
keywords:
- 绘制内核模式视频传输 WDK DirectDraw，用户模式下处理
- DirectDraw 内核模式视频传输 WDK Windows 2000 显示，用户模式下处理
- 视频传输 WDK DirectDraw 的内核模式下，用户模式下处理
- 视频传输内核模式 WDK DirectDraw，用户模式下句柄
- 用户模式下处理 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ed2f4ce982b43af8659a7a5207fabc1da1a2985
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379977"
---
# <a name="getting-the-user-mode-handles"></a>获取用户模式句柄


## <span id="ddk_getting_the_user_mode_handles_gg"></span><span id="DDK_GETTING_THE_USER_MODE_HANDLES_GG"></span>


以下过程介绍如何获取用户模式 (ring 3) 句柄。

若要获取 DirectDraw 句柄 DirectDraw 对象：

1. 调用**QueryInterface (** <em>lpDD</em>，&*IID\_IDirectDrawKernel*，&<em>pNewInterface</em> **)** DirectDraw 接口上。

2. 调用[ **IDirectDrawKernel::GetKernelHandle** ](https://docs.microsoft.com/windows/desktop/api/ddkernel/nf-ddkernel-idirectdrawkernel-getkernelhandle)新接口上的方法。

**IDirectDrawKernel::GetKernelHandle**方法返回 DirectDraw 对象的内核模式句柄。 若要释放句柄，请使用[ **IDirectDrawKernel::ReleaseKernelHandle** ](https://docs.microsoft.com/windows/desktop/api/ddkernel/nf-ddkernel-idirectdrawkernel-releasekernelhandle)方法。

用户模式组件还可以调用[ **IDirectDrawKernel::GetCaps** ](https://docs.microsoft.com/windows/desktop/api/ddkernel/nf-ddkernel-idirectdrawkernel-getcaps)方法来检索 DirectDraw 对象的内核模式功能。

### <a name="span-idcodesamplespanspan-idcodesamplespancode-sample"></a><span id="code_sample"></span><span id="CODE_SAMPLE"></span>代码示例

```cpp
ddRVal = IDirectDraw_QueryInterface( lpDD, &IID_IDirectDrawKernel, &pDDK );
if( ( ddRVal == DD_OK ) && ( pDDK != NULL ) )
{
    dwDirectDrawHandle = 0;
    IDirectDrawKernel_GetKernelHandle( pDDK, dwDirectDrawHandle );
    if( dwDirectDrawHandle == 0 )
    {
        // error
    }
}
```

若要获取 DirectDrawSurface 句柄：

1. 调用**QueryInterface (** <em>lpSurface</em>，&*IID\_IDirectDrawSurfaceKernel*，&<em>pDDSK</em> **)** DirectDrawSurface 接口上。

2. 调用[ **IDirectDrawSurfaceKernel::GetKernelHandle** ](https://docs.microsoft.com/windows/desktop/api/ddkernel/nf-ddkernel-idirectdrawsurfacekernel-getkernelhandle)新接口上的方法。

**IDirectDrawSurfaceKernel::GetKernelHandle**方法返回 DirectDrawSurface 驱动程序的内核模式句柄。 若要释放句柄，请使用[ **IDirectDrawSurfaceKernel::ReleaseKernelHandle** ](https://docs.microsoft.com/windows/desktop/api/ddkernel/nf-ddkernel-idirectdrawsurfacekernel-releasekernelhandle)方法。

### <a name="span-idcodesample2spanspan-idcodesample2spancode-sample"></a><span id="code_sample2"></span><span id="CODE_SAMPLE2"></span>代码示例

```cpp
ddRVal = IDirectDraw_QueryInterface( lpSurface,
             &IID_IDirectDrawSurfaceKernel, &pDDSK );
if( ( ddRVal == DD_OK ) && ( pDDK != NULL ) )
{
    dwSurfaceHandle = 0;
    IDirectDrawSurfaceKernel_GetKernelHandle( pDDSK, dwSurfaceHandle );
    if( dwSurfaceHandle == 0 )
    {
        // error
    }
}
```

 

 






---
title: 获取用户模式句柄
description: 获取用户模式句柄
keywords:
- 绘制内核模式视频传输 WDK DirectDraw，用户模式句柄
- DirectDraw 内核模式视频传输 WDK Windows 2000 显示，用户模式句柄
- 内核模式视频传输 WDK DirectDraw，用户模式句柄
- 视频传输内核模式 WDK DirectDraw，用户模式句柄
- 用户模式处理 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad631271f815efbe7206370502a86b75d68d6e22
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819587"
---
# <a name="getting-the-user-mode-handles"></a>获取用户模式句柄


## <span id="ddk_getting_the_user_mode_handles_gg"></span><span id="DDK_GETTING_THE_USER_MODE_HANDLES_GG"></span>


下面的过程演示如何获取用户模式 (ring 3) 句柄。

获取 DirectDraw 对象的 DirectDraw 句柄：

1. 在 DirectDraw 接口上调用 **QueryInterface (** <em>LpDD</em>，&*IID \_ IDirectDrawKernel*，&<em>pNewInterface</em> **)** 。

2. 调用新接口上的 [**IDirectDrawKernel：： GetKernelHandle**](/windows/win32/api/ddkernel/nf-ddkernel-idirectdrawkernel-getkernelhandle) 方法。

**IDirectDrawKernel：： GetKernelHandle** 方法返回 DirectDraw 对象的内核模式句柄。 若要释放句柄，请使用 [**IDirectDrawKernel：： ReleaseKernelHandle**](/windows/win32/api/ddkernel/nf-ddkernel-idirectdrawkernel-releasekernelhandle) 方法。

用户模式组件还可以调用 [**IDirectDrawKernel：： GetCaps**](/windows/win32/api/ddkernel/nf-ddkernel-idirectdrawkernel-getcaps) 方法来检索 DirectDraw 对象的内核模式功能。

### <a name="span-idcode_samplespanspan-idcode_samplespancode-sample"></a><span id="code_sample"></span><span id="CODE_SAMPLE"></span>代码示例

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

获取 DirectDrawSurface 句柄：

1. 调用 **QueryInterface (** <em>LpSurface</em>，&*IID \_ IDirectDrawSurfaceKernel*，&<em>pDDSK</em> **)** 在 DirectDrawSurface 接口上。

2. 调用新接口上的 [**IDirectDrawSurfaceKernel：： GetKernelHandle**](/windows/win32/api/ddkernel/nf-ddkernel-idirectdrawsurfacekernel-getkernelhandle) 方法。

**IDirectDrawSurfaceKernel：： GetKernelHandle** 方法返回 DirectDrawSurface 驱动程序的内核模式句柄。 若要释放句柄，请使用 [**IDirectDrawSurfaceKernel：： ReleaseKernelHandle**](/windows/win32/api/ddkernel/nf-ddkernel-idirectdrawsurfacekernel-releasekernelhandle) 方法。

### <a name="span-idcode_sample2spanspan-idcode_sample2spancode-sample"></a><span id="code_sample2"></span><span id="CODE_SAMPLE2"></span>代码示例

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

 


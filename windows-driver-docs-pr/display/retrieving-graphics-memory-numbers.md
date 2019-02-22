---
title: 检索图形内存数字
description: 检索图形内存数字
ms.assetid: ec704093-ad9a-4717-8e9e-537a2848b1c7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2af0b2d0d88f7f1b1761d47ea97b927afcc1b1f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522221"
---
# <a name="retrieving-graphics-memory-numbers"></a>检索图形内存数字


软件开发人员创建图形应用程序可以使用启动 Windows Vista 中的 Microsoft DirectX 版本 10 Api 来检索运行的计算机上的图形内存数字的精确的一组[Windows 显示器驱动程序模型 (WDDM)](windows-vista-display-driver-model-design-guide.md)显示驱动程序。 以下步骤演示如何检索图形内存号码：

1.  由于新的图形内存报告仅在运行 Windows 显示驱动程序模型 (WDDM) 显示器驱动程序的计算机上可用，应用程序必须先调用以下函数以确认驱动程序模型：
    ```cpp
    HasWDDMDriver()
    {
        LPDIRECT3DCREATE9EX pD3D9Create9Ex = NULL;
        HMODULE             hD3D9          = NULL;

        hD3D9 = LoadLibrary( L"d3d9.dll" );

        if ( NULL == hD3D9 ) {
            return false;
        }

        //
        //  Try to create a IDirect3D9Ex interface (also known as a DX9L 
        //  interface).
        //  This interface can only be created if the driver is written 
        //  according to the Windows Display Driver Model (WDDM).
        //
        pD3D9Create9Ex = (LPDIRECT3DCREATE9EX) GetProcAddress (
            hD3D9, "Direct3DCreate9Ex" );

        return pD3D9Create9Ex != NULL;
    }
    ```

2.  应用程序确定了显示器驱动程序模型是 WDDM 后，应用程序可以使用新的 DirectX 版本 10 Api 来获取图形内存数字。 应用程序从下列选项中获取图形内存数字[ **DXGI\_适配器\_DESC** ](https://msdn.microsoft.com/library/windows/desktop/bb173058)数据结构，它是位于 Dxgi.h，包含在 DirectX软件开发工具包 (SDK)。
    ```cpp
    typedef struct DXGI_ADAPTER_DESC {
        WCHAR Description[ 128 ];
        UINT VendorId;
        UINT DeviceId;
        UINT SubSysId;
        UINT Revision;
        SIZE_T DedicatedVideoMemory;
        SIZE_T DedicatedSystemMemory;
        SIZE_T SharedSystemMemory;
        LUID AdapterLuid;
        } DXGI_ADAPTER_DESC;
    ```

由于在 Windows Vista 和更高版本的桌面和 DirectX 游戏图形的广泛使用，运行 Windows Vista 及更高版本的软件应该能够准确地确定可用的图形内存量。 WDDM 管理的虚拟化本身的图形内存，并还将确保准确报告图形内存的各个方面。 应用程序开发人员和软件供应商应充分利用的 DirectX 版本 10 Api 用于检索具有 Windows Vista 的计算机上的图形内存值的精确的一组显示驱动程序。


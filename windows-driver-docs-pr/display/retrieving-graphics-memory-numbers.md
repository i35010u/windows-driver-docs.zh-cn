---
title: 检索图形内存数字
description: 检索图形内存数字
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e8a67dc91f3f2f201ca1e6acbbf47ea48458214
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824205"
---
# <a name="retrieving-graphics-memory-numbers"></a>检索图形内存数字


创建图形应用程序的软件开发人员可以使用 Windows Vista 中的 Microsoft DirectX 版本 10 Api 在运行 [Windows 显示驱动程序模型 (WDDM) ](windows-vista-display-driver-model-design-guide.md) 显示驱动程序的计算机上检索准确的图形内存编号集。 以下步骤演示了如何检索图形内存编号：

1.  由于新的图形内存报告仅在运行 Windows 显示驱动程序模型 (WDDM) 显示驱动程序的计算机上可用，因此应用程序必须先调用以下函数以确认驱动程序模型：
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

2.  在应用程序确定显示器驱动程序模型为 WDDM 后，应用程序可以使用新的 DirectX 版本 10 Api 来获取图形内存号。 应用程序从以下 [**dxgi \_ 适配器 \_ DESC**](/windows/win32/api/dxgi/ns-dxgi-dxgi_adapter_desc) 数据结构中获取图形内存编号，该数据结构存在于 dxgi 中，并包含在 (SDK) 的 DirectX 软件开发工具包中。
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

由于 Windows Vista 及更高版本的桌面版和 DirectX 游戏中的图形广泛使用，在 Windows Vista 和更高版本上运行的软件应能准确确定可用的图形内存量。 WDDM 管理自身的图形内存虚拟化，并且还可以确保准确报告图形内存的各个方面。 应用程序开发人员和软件供应商应当利用 DirectX 版本 10 Api 来检索具有 Windows Vista 显示器驱动程序的计算机上准确的图形内存值集。

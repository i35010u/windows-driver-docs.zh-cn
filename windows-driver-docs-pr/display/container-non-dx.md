---
title: 容器支持非 DX Api
description: 非 DX Api 必须与驱动程序和内核更直接交互，因此它们公开给更多的并发数据
ms.assetid: 6c4a6974-c67b-4710-80c6-48a5b378e088
ms.date: 04/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: a101d1891100403bf633882856ccb3b00a531d26
ms.sourcegitcommit: 944535d8e00393531f6b265317a64da3567e4f2c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65106414"
---
# <a name="container-support-for-non-dx-apis"></a>容器支持非 DX Api

Windows 10 添加了一些功能，显著影响非 DX Api，以及它们依赖于较低级别 WDDM 体系结构详细功能。
1. 半虚拟化 WDDM 适配器 
2. 用户现在可以控制使用不区分自己的应用程序的适配器
3. [通用驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)引入了一组新的设计原则

保持与最新的 Windows 10 功能的兼容性需要进行以下修改：

必须通过间接访问的注册表和驱动程序存储区[D3DKMTQueryAdapterInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtqueryadapterinfo)与[KMTQAITYPE_QUERYREGISTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ne-d3dkmthk-_kmtqueryadapterinfotype)，并[D3DDDI_QUERYREGISTRY_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_queryregistry_info)。

默认的适配器必须接受用户的选择，这要求：
1. 枚举通过 DXGI 的适配器[IDXGIFactory::EnumAdapters](https://docs.microsoft.com/windows/desktop/api/dxgi/nf-dxgi-idxgifactory-enumadapters)，如 DXGI 遵循用户的选择。 基于适配器 0 更改[用户的设置](https://blogs.windows.com/windowsexperience/2018/02/07/announcing-windows-10-insider-preview-build-17093-pc/)。
2. 与获得的适配器顺序一致[D3DKMTEnumAdapters2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtenumadapters2)到 DXGI 的。
适配器标识就相符了通过关联这两种枚举技术之间的 LUID。
DXGI 返回通过其 LUID [IDXGIAdapter::GetDesc](https://docs.microsoft.com/windows/desktop/api/dxgi/nf-dxgi-idxgiadapter-getdesc)。

尽可能，可能会不同基于支持的确切设备接受任意数量的通用驱动程序设计原则。

## <a name="wdk-dependency"></a>WDK 依赖关系

许多先前提到的方法和类型是 WDK，用于生成驱动程序中以独占方式可用。
这是 Microsoft 的标头，组织中令人遗憾监督，因为非 DX Api 之前无法依赖于只是 Windows SDK。
如果它是太繁重的非 DX Api 包括 WDK 或本地化的运行时或加载程序组件到 WDK 依赖项，然后 Microsoft 不提供 DX API 项目的权限来有效地 sever WDK 依赖关系。
通过使用 Microsoft 的公共文档，并创建二进制文件兼容的类型和函数声明到自己的项目，可以被切断 WDK 依赖关系。
这些 typenames 不能与 Microsoft，用于避免名称冲突，如果其他人有意利用 DX API 项目 WDK 的相同。


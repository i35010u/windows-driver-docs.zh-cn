---
title: 容器支持非 DX Api
description: 非 DX Api 必须与驱动程序和内核更直接交互，因此它们公开给更多的并发数据
ms.assetid: 6c4a6974-c67b-4710-80c6-48a5b378e088
ms.date: 05/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: ed5ff1d1438f20c225076c608d6c7a3e264d5b3b
ms.sourcegitcommit: 0c364a5c4947fcfe815de5fb57237c3e36b3ae20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65701992"
---
# <a name="container-support-for-non-dx-apis"></a>容器支持非 DX Api

Windows 10 添加了一些功能，显著影响非 DX Api，以及它们依赖于较低级别 WDDM 体系结构详细功能。
1. 半虚拟化 WDDM 适配器 
2. 用户现在可以控制使用不区分自己的应用程序的适配器
3. [通用驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)引入了一组新的设计原则

保持与最新的 Windows 10 功能的兼容性需要进行以下修改：

## <a name="driver-inf-modifications"></a>驱动程序 INF 修改
该驱动程序必须将非 DX 运行时注册到相应的注册表位置，其二进制文件安装到 Windows 安装的 system32 和 syswow64 子目录。
在安装 INF 中，该驱动程序可以定义多个值中的图形适配器注册表项下的子键：
- CopyToVmOverwrite
- CopyToVmWhenNewer
- CopyToVmOverwriteWow64
- CopyToVmWhenNewerWow64

前一个子键修改 system32 目录中，而后者子密钥修改 syswow64 目录。
__更高版本__定义的文件进行比较[ChangeTime](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_basic_information)。
子项下的每个值类型必须为 REG_MULTI_SZ 或 REG_SZ。 如果值类型是 REG_MULTI_SZ，值中必须是最大的两个字符串。 这意味着每个值定义一对的字符串，其中第二个字符串的可为空。
一对中的第一个名称是驱动程序存储区中的文件的路径。 路径是相对于根的驱动程序存储区，可以包含子目录。
一对中的第二个名称是文件的在 system32 或 syswow64 目录中的外观的名称。
第二个名称必须是文件名，不包括路径。 如果第二个名称为空，则文件名称是与 （不包括子目录） 驱动程序存储区中的相同。
这将允许驱动程序在来宾和主机驱动程序存储区中有不同的名称。 

### <a name="example-1"></a>示例 1：
[服务安装节] INF 部分  
HKR, "softgpukmd\CopyToVmOverwrite", SoftGpuFiles, %REG_MULTI_SZ%, "CopyToVm\softgpu1.dll", "softgpu2.dll"  

该指令将服务密钥在创建注册表项："HKLM\SYSTEM\CurrentControlSet\Services\softgpukmd\CopyToVmOverwrite", SoftGpuFiles = REG_MULTI_SZ, "CopyToVm\softgpu1.dll", "softgpu2.dll"

操作系统会将复制\<DriverStorePath > 到 %windir%\system32\softgpu2.dll \CopyToVm\softgpu1.dll

### <a name="example-2"></a>示例 2：
INF [DDInstall] 部分中：  
HKR, "CopyToVmOverwrite", SoftGpuFiles1, %REG_MULTI_SZ%, "softgpu1.dll", "softgpu.dll"  
HKR, "CopyToVmOverwrite", SoftGpuFiles2, %REG_SZ%, "softgpu2.dll"  

该指令将在软件 （适配器） 项中创建注册表项：  
"HKLM\SYSTEM\CurrentControlSet\Control\Class\\{4d36e968-e325-11ce-bfc1-08002be10318}\\\<number>\CopyToVmOverwrite", SoftGpuFiles1 = REG_MULTI_SZ, "softgpu1.dll", "softgpu.dll"  
"HKLM\SYSTEM\CurrentControlSet\Control\Class\\{4d36e968-e325-11ce-bfc1-08002be10318}\\\<number>\CopyToVmOverwrite", SoftGpuFiles = REG_SZ, "softgpu2.dll"  

将复制 OS \<DriverStorePath > 到 %windir%\system32\softgpu.dll \softgpu1.dll 和\<DriverStorePath > 到 %windir%\system32\softgpu2.dll \softgpu2.dll

### <a name="example-3"></a>示例 3：
INF [DDInstall] 部分中：  
HKR, "CopyToVmOverwriteWow64", SoftGpuFiles, %REG_MULTI_SZ%, "Subdir1\Subdir2\softgpu2wow64.dll", "softgpu.dll"  

该指令将在软件 （适配器） 项中创建注册表项：  
"HKLM\SYSTEM\CurrentControlSet\Control\Class\\{4d36e968-e325-11ce-bfc1-08002be10318}\\\<数 > \CopyToVmOverwriteWow64"，SoftGpuFiles = REG_MULTI_SZ，"Subdir1\Subdir2\softgpu2wow64.dll""softgpu.dll"  

操作系统会将复制\<DriverStorePath > 到 %windir%\syswow64\softgpu.dll \Subdir1\Subdir2\softgpu2wow64.dll

## <a name="driver-modifications-to-registry-and-file-paths"></a>对注册表和文件路径的驱动程序进行修改
在容器，驱动程序存储区不是始终位于相同的规范路径通常是。
若要一致地使用正确调整后的路径，注册表和驱动程序存储区必须访问间接通过[D3DKMTQueryAdapterInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtqueryadapterinfo)与[KMTQAITYPE_QUERYREGISTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ne-d3dkmthk-_kmtqueryadapterinfotype)，和[D3DDDI_QUERYREGISTRY_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_queryregistry_info)。

## <a name="honor-os-default-adapter-setting"></a>遵循操作系统默认适配器设置
默认的适配器必须遵循在 OS 中，这需要存储的用户的选择：
1. 枚举通过 DXGI 的适配器[IDXGIFactory::EnumAdapters](https://docs.microsoft.com/windows/desktop/api/dxgi/nf-dxgi-idxgifactory-enumadapters)，如 DXGI 遵循用户的选择。 基于适配器 0 更改[用户的设置](https://blogs.windows.com/windowsexperience/2018/02/07/announcing-windows-10-insider-preview-build-17093-pc/)。
2. 与获得的适配器顺序一致[D3DKMTEnumAdapters2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtenumadapters2)到 DXGI 的。
适配器标识就相符了通过关联这两种枚举技术之间的 LUID。
DXGI 返回通过其 LUID [IDXGIAdapter::GetDesc](https://docs.microsoft.com/windows/desktop/api/dxgi/nf-dxgi-idxgiadapter-getdesc)。

## <a name="dchu-design-modifications"></a>DCHU 将设计修改
接受任意数量[通用驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)设计为尽可能，可能会不同基于完全受支持的设备上的主体。

## <a name="wdk-dependency"></a>WDK 依赖关系

许多先前提到的方法和类型是 WDK，用于生成驱动程序中以独占方式可用。
这是 Microsoft 的标头，组织中令人遗憾监督，因为非 DX Api 之前无法依赖于只是 Windows SDK。
如果它是太繁重的非 DX Api 包括 WDK 或本地化的运行时或加载程序组件到 WDK 依赖项，然后 Microsoft 不提供 DX API 项目的权限来有效地 sever WDK 依赖关系。
通过使用 Microsoft 的公共文档，并创建二进制文件兼容的类型和函数声明到自己的项目，可以被切断 WDK 依赖关系。
这些 typenames 不能与 Microsoft，用于避免名称冲突，如果其他人有意利用 DX API 项目 WDK 的相同。


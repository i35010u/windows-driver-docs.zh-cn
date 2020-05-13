---
title: 容器对非 DX Api 的支持
description: 非 DX Api 必须更直接与驱动程序和内核交互，因此它们的复杂性更高
ms.assetid: 6c4a6974-c67b-4710-80c6-48a5b378e088
ms.date: 05/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 34681000436867dae50f9c838e96412679138384
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235397"
---
# <a name="container-support-for-non-dx-apis"></a>容器对非 DX Api 的支持

Windows 10 添加了多个功能，这些功能明显影响非 DX Api，还增加了它们依赖的更低级别的 WDDM 体系结构详细信息。
1. 半虚拟化 WDDM 适配器 
2. 用户现在可以控制不区分自身的应用程序所使用的适配器
3. [通用驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)引入了一组新的设计原则

若要保持与最新的 Windows 10 功能的兼容性，需要进行以下修改：

## <a name="driver-inf-modifications"></a>驱动程序 INF 修改
驱动程序必须将非 DX 运行时注册到相应的注册表位置，以将其二进制文件安装到 Windows 安装的 system32 和 syswow64 子目录中。
在安装 INF 中，驱动程序可以在图形适配器注册表项的下列子项中定义多个值：
- CopyToVmOverwrite
- CopyToVmWhenNewer
- CopyToVmOverwriteWow64
- CopyToVmWhenNewerWow64

以前的子键会修改 system32 目录，而后一子项会修改 syswow64 目录。
子项下的每个值类型都必须 REG_MULTI_SZ 或 REG_SZ。 如果值类型为 REG_MULTI_SZ，则值中必须包含最多2个字符串。 这意味着每个值都定义了一对 stings，其中的第二个字符串可能为空。
对中的第一个名称是指向驱动程序存储区中的文件的路径。 路径相对于驱动程序存储区的根路径，可以包含子目录。
对中的第二个名称是文件的名称，该名称将显示在 system32 或 syswow64 目录中。
第二个名称必须只是文件名，不能包含路径。 如果第二个名称为空，则文件名与驱动程序存储区中的名称相同（子目录除外）。
这使得驱动程序可以在主机驱动程序存储和来宾中具有不同的名称。 

**CopyToVmWhenNewer**和**CopyToVmWhenNewerWow64**图形适配器注册表子项下列出的文件仅在满足 "较新的" 条件时覆盖目标文件。

在 Windows 10 版本2004中，"更新" 条件比较了两部分信息：
- [FileVersion](https://docs.microsoft.com/windows/desktop/api/verrsrc/ns-verrsrc-vs_fixedfileinfo)
- [LastWriteTime](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_basic_information)

如果目标文件以 .dll 或 .exe 后缀结尾，则会将**FileVersion**用作最高的比较值，在此值中，最大版本被认为是 "较新的"。

如果目标文件不以 .dll 或 .exe 后缀结尾，或者两个**FileVersion**相等，则**LastWriteTime**将用作最小重要比较值，在这种情况下，以后的日期/时间被认为是 "较新的"。

在早于2004的 Windows 10 版本中，"新的" 条件仅比较了文件 " [ChangeTime](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_basic_information)"。

### <a name="example-1"></a>示例 1：
INF [DDInstall] 部分  
HKR、"softgpukmd\CopyToVmOverwrite"、SoftGpuFiles、% REG_MULTI_SZ%、"CopyToVm\softgpu1.dll"、"softgpu2"  

指令将在软件（适配器）项中创建注册表项： "HKLM\SYSTEM\CurrentControlSet\Control\Class \\ {4d36e968-e325-11ce-bfc1-08002be10318} \\ \< number> \Copytovmoverwrite"，SoftGpuFiles = REG_MULTI_SZ，"CopyToVm\softgpu1.dll"，"softgpu2"

OS 会将 \< DriverStorePath> \copytovm\softgpu1.dll 复制到%windir%\system32\softgpu2.dll

### <a name="example-2"></a>示例 2：
INF [DDInstall] 部分：  
HKR、"CopyToVmOverwrite"、SoftGpuFiles1、% REG_MULTI_SZ%、"softgpu1"、"softgpu"  
HKR、"CopyToVmOverwrite"、SoftGpuFiles2、% REG_SZ%、"softgpu2"  

指令将在软件（适配器）密钥中创建注册表项：  
"HKLM\SYSTEM\CurrentControlSet\Control\Class \\ {4d36e968-e325-11ce-bfc1-08002be10318} \\ \< number> \Copytovmoverwrite"，SoftGpuFiles1 = REG_MULTI_SZ，"softgpu1"，"softgpu"  
"HKLM\SYSTEM\CurrentControlSet\Control\Class \\ {4d36e968-e325-11ce-bfc1-08002be10318} \\ \< number> \Copytovmoverwrite"，SoftGpuFiles = REG_SZ，"softgpu2"  

OS 会将 \< DriverStorePath> \softgpu1.dll 复制到%windir%\system32\softgpu.dll， \< DriverStorePath> \softgpu2.dll 复制到%windir%\system32\softgpu2.dll

### <a name="example-3"></a>示例 3：
INF [DDInstall] 部分：  
HKR、"CopyToVmOverwriteWow64"、SoftGpuFiles、% REG_MULTI_SZ%、"Subdir1\Subdir2\softgpu2wow64.dll"、"softgpu"  

指令将在软件（适配器）密钥中创建注册表项：  
"HKLM\SYSTEM\CurrentControlSet\Control\Class \\ {4d36e968-e325-11ce-bfc1-08002be10318} \\ \< number> \Copytovmoverwritewow64"，SoftGpuFiles = REG_MULTI_SZ，"Subdir1\Subdir2\softgpu2wow64.dll"，"softgpu"  

OS 会将 \< DriverStorePath> \subdir1\subdir2\softgpu2wow64.dll 复制到%windir%\syswow64\softgpu.dll

## <a name="driver-modifications-to-registry-and-file-paths"></a>注册表和文件路径的驱动程序修改
在容器中，驱动程序存储区并不一致地位于与通常相同的规范路径中。
若要一致地使用正确调整的路径，必须使用[KMTQAITYPE_QUERYREGISTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ne-d3dkmthk-_kmtqueryadapterinfotype)和[D3DDDI_QUERYREGISTRY_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_queryregistry_info)通过[D3DKMTQueryAdapterInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtqueryadapterinfo)间接访问注册表和驱动程序存储区。

## <a name="honor-os-default-adapter-setting"></a>遵循 OS 默认适配器设置
默认适配器必须遵循操作系统中存储的用户选择，这需要：
1. 通过 DXGI 的[IDXGIFactory：： EnumAdapters](https://docs.microsoft.com/windows/desktop/api/dxgi/nf-dxgi-idxgifactory-enumadapters)枚举适配器，因为 dxgi 是用户的选择。 适配器0根据[用户的设置](https://blogs.windows.com/windowsexperience/2018/02/07/announcing-windows-10-insider-preview-build-17093-pc/)进行了更改。
2. 使适配器从[D3DKMTEnumAdapters2](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtenumadapters2)到 DXGI 的顺序匹配。
可以通过关联两个枚举技术之间的 LUID 来匹配适配器标识。
DXGI 通过[IDXGIAdapter：： GetDesc](https://docs.microsoft.com/windows/desktop/api/dxgi/nf-dxgi-idxgiadapter-getdesc)返回其 LUID。

## <a name="dchu-design-modifications"></a>DCHU 设计修改
请考虑尽可能多的[通用驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)设计主体，这可能会根据所支持的确切设备而有所不同。

## <a name="d3dkmt-headers"></a>D3DKMT 标头
Windows 10 版本2004和更高版本 Windows SDK 中提供了包含上述方法和类型的标头，而不是在 WDK 中独占使用。

要完全包含所需标头的一个选项如下所示。
其他选项也可能存在。
```cpp
// Turn off NTSTATUS codes within windows.h, so that the more exhaustive ntstatus.h can be used.
#define UMDF_USING_NTSTATUS
#include <windows.h> // For the vast majority of Windows functionality
#include <winternl.h> // For NT_SUCCESS
#include <ntstatus.h> // For the most exhaustive list of NTSTATUS codes
#include <d3dkmthk.h> // For D3DKMT support
```

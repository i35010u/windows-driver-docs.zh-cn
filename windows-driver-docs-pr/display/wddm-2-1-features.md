---
title: WDDM 2.1 功能
description: 本部分提供有关新功能和增强功能在 Windows 显示驱动程序模型 (WDDM) 2.1 版的详细信息。
ms.assetid: 7dc0d0ad-98da-4bd6-bed9-f70525b682bc
ms.date: 01/10/2019
ms.localizationpriority: medium
ms.openlocfilehash: 9299bf0a565c4765c1cfe506c6e4fdc513cd0a08
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547226"
---
# <a name="wddm-21-features"></a>WDDM 2.1 功能


本主题提供有关新功能和增强功能在 Windows 显示驱动程序模型 (WDDM) 版本 2.1 的详细信息，这是从 Windows 10 周年纪念版开始提供。

WDDM 2.1 本身是可选的。 如果实现，它是必需的和可选驱动程序功能的集合。 支持任何这些功能的任何驱动程序必须支持所有必需的。  支持可以验证 HLK 测试通过但 Dxgkrnl 将中的功能和 DDIs 的一致性检查。

**WDDM 2.1 要求表**

| 功能 | 适用性 |
| --- | --- |
| 提供和回收改进 | 强制 |
| 视频内存管理 | 可选 |
| HW 受保护内容的可靠性改进 | 选择硬件 |
| Windows GameDVR 的应用程序支持 | 强制 |
| 间接显示 | 选择硬件 |
| 驱动程序存储区并通过并行安装 | 强制 |
| DirectX 的照相机/捕获方案共享的内存图面 | 强制|

WDDM 2.1 支持以下 D3D 版本：D3D9、 D3D10、 D3D10.1、 D3D11、 D3D11.x、 D3D12

## <a name="offer-and-reclaim-improvements"></a>提供和回收改进

新 DDI [PFND3DDDI_RECLAIMALLOCATIONS3CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimallocations3cb)创建以减少内存占用量在后台模式下运行的应用程序。 此接口将使应用程序提供了可接受要完全取消提交，请转到在后台时的资源。 因此，进程生存期管理器能够回收从使用 DirectX，这将导致较少内存压力下的后台应用程序终止的后台应用程序的更多内存。

其他 DDI 的更改：

* [PFND3DDDI_UPDATEALLOCATIONPROPERTYCB 回调](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_updateallocationpropertycb)
* [PFND3DDDI_OFFERALLOCATIONS2CB 回调](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_offerallocations2cb)
* [D3DDDICB_OFFERALLOCATIONS2 结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-d3dddicb_offerallocations2)
* [D3DDDICB_RECLAIMALLOCATIONS3 结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_reclaimallocations3)

有关详细信息提供和回收资源，请参阅[产品/服务并回收更改](offer-and-reclaim-changes.md)。

## <a name="application-support-with-windows-gamedvr"></a>Windows GameDVR 的应用程序支持

Windows 10 周年纪念版包括与全屏幕的游戏中使用了 Windows 游戏栏和 GameDVR 改进的功能。

WDDM 2.1 驱动程序支持所需调用的性能特点*提供批处理*，这增加了对翻转模式交换链的多线程处理支持。 这是性能的一项基本功能，以确保该全屏游戏具有在相同级别与在早期版本的 Windows 上运行的游戏栏。

下面列出了新 DDIs 创建以启用此功能：

* [PFND3DDDI_SYNCTOKENCB 回调](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_synctokencb)
* [D3DDDIARG_SYNCTOKEN 结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_synctoken)
* [PFND3DDDI_SYNCTOKEN 回调](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_synctoken)


## <a name="indirect-display"></a>间接显示

在 WDDM 2.1 间接显示允许 USB 连接显示参与所有相同的用户体验与任何其他监视器。 此外，间接显示驱动程序是用户模式驱动程序，这是开发比简单的内核模式驱动程序，因此可能会导致更高的整体系统可靠性。

WDDM 2.1 中，会启用以下 USB 显示功能/体验：

* 在连接 USB 显示到 Windows 平台或升级操作系统，正确的驱动程序将下载并安装来自 Windows 更新。

* 连接到 USB 显示硬件的监视器将检测并拓扑、 分辨率和 DPI 设置了正确的监视器。

* 用户可以更改监视器分辨率和缩放在监视器上。

* 用户可以断开 USB 显示和重新连接不会产生意外的副作用的显示。

* 保留监视器拓扑通过断开连接，然后重新连接到相同的监视器。

* USB 包括睡眠和休眠状态的各种电源状态中正确显示函数。

有关间接显示详细信息，请参阅[间接显示驱动程序模型概述](indirect-display-driver-model-overview.md)

## <a name="driver-store-and-side-by-side-driver-installation"></a>驱动程序存储区并通过并行驱动程序安装

WDDM 2.1 引入了通过图形驱动程序安装*驱动程序存储区*。 安装图形驱动程序的这种机制提高了从 Windows 更新，消除导致系统不稳定这些现象的驱动程序文件版本不匹配的驱动程序更新的复原能力，用户启动重新启动。 将直接从驱动程序存储区中的唯一位置运行每个后续的驱动程序更新 (即`System32\DriverStore\FileRepository\[…]`)，从而避免驱动程序文件，则覆盖并不匹配。

驱动程序存储区的功能实现需要对图形驱动程序 INF 文件的更改才能确保，驱动程序文件复制到唯一的驱动程序存储库。 更详细地介绍了 INF 更改[INF 要求](#graphics-inf-requirements)本文档中的部分。

## <a name="dxil"></a>DXIL

WDDM 2.1 引入了 GPU 着色器编译器堆栈的转换从 DirectX 字节代码 (DXBC) 到 DirectX 中间语言 (DXIL)，用于传输到 GPU 的着色器说明的新格式。 过渡到 DXIL 为开发人员提供以下优势：

* 改进了可编程性的简化开发，着色器创建过程的复杂性降低了开发人员最大程度减少 GPU 编程语法和开发人员都熟悉的 CPU 语言之间的差异。

* 性能更高的编译器： 

    * *着色器的运行时性能*能够提高性能。 
    * DXIL 提供了一组新的内部函数，使数据间共享单指令多数据处理器的通道在 Gpu 中。

* 工作流的灵活性-DXIL 使开发人员能够控制其自己的自定义工具和优化传递，并选择在生成时与运行时应用的编译步骤。

* 高级语言功能的改进的语言提供以下主要功能消除 GPU 和 CPU 代码之间的差异并平展的 GPU 编程人员的学习曲线。

借助这些功能，将重点放在为开发人员提供的好处，最终用户将看到中改进了新的或更新游戏甚至当在现有硬件上运行的性能优势。

## <a name="directx-memory-surface-sharing-for-cameracapture-scenarios"></a>对于相机捕捉/方案共享的 DirectX 内存图面

WDDM 2.1 中引入了一个框架服务器组件来共享照相机或同时捕获跨多个进程的设备。 这使保存的捕获的帧到多个应用程序可以读取的位置，而不是复制多个时间的进程和共同的进程之间的图像数据的一个内存位置。 此功能提供更有效地管理捕获图片跨多个进程、 节能、 降低带宽和更低的延迟 WDDM 2.1 符合硬件和驱动程序中的性能提升的结果为应用程序和用户。

帧服务器分配捕获的映像作为跨进程可共享内存，并共享此内存进程请求访问。 值得注意的是，因为帧服务器会广播到多个客户端进程的纹理，纹理必须支持并发读取它。 目前 NV12 纹理支持实现此目的。

## <a name="pipeline-state-object-pso-caching-and-library"></a>管道状态对象 (PSO) 缓存和库

D3D12 中引入，管道状态对象 (PSO) 是一个接口表示图形管道的说明和资源 （也称为状态） 作为统一对象以减少 D3D 和驱动程序分解的状态不匹配。 运行以图形方式要求苛刻的应用程序和游戏需要创建大量的 Pso。 

WDDM 2.1 PSO 库和缓存使游戏应用程序在最初运行时创建后将在物理存储上的 PSO。 这样，D3D 运行时库在将来实例从而减少 PSO 提取时间中检索预先创建的 Pso 的功能。 例如，运行时游戏后第一次或重新启动 PC 后，内容将从物理库作为加载已保存的 Pso。


## <a name="start-of-pipeline-gpu-timestamps"></a>管道 GPU 时间戳的开始

WDDM 2.1 中引入的功能，若要获取的 GPU 管道中的图形事件的时间戳的开始。 此新功能，结合使用的管道的时间戳，结尾为开发人员提供清晰而细粒度的并行化，可视化借助管道传输，以及计时的 GPU 上发生的应用程序的活动。 提供与每个事件的执行时间，开发人员可以进一步优化了代码并调查效率低下和其他性能问题。

此功能可能会导致启用 '实时、 低开销' GPU 性能数据收集和在此同时，提供了足够的信息来可视化和度量值的 Gpu 上的工作负荷。 功能的目标是提供足够的信息来重新构造的确切顺序和执行由 GPU，以便工具可以可视化并行性和使用引擎时，管道的操作的持续时间测量 GPU 工作负荷，并确定潜在同步问题。

## <a name="viewing-gpu-microcode"></a>查看 GPU 微代码，

WDDM 2.1 开发人员可以通过提供 GPU 微代码，查看来进一步优化其着色器。 开发人员编程通过在 HLSL 中, 创建着色器图形管道随后编译到 GPU 驱动程序的中间语言。 该驱动程序在运行其他编译和优化功能，可将此代码转换为特定于 GPU 的说明，其中会保持不透明的开发人员。 使用此功能，开发人员提供可读的特定于 GPU 的代码以评估其着色器优化和速度的程度。

此功能使 UMD （又对每个可编程的图形管道阶段发表评论。 着色器） 和回报程序员的使用或不恰当使用这些着色器的可操作的信息。 特定于 GPU 的微代码，是拆装，并显示在可读的字符串格式以及 UMD 注释。 开发人员可以查看其 HLSL 代码映射到可读 GPU 代码同时使其能够动态修改其代码和 GPU 代码端看到的编译器优化结果。

## <a name="determining-wddm-version"></a>确定 WDDM 版本

### <a name="wddm-21-caps"></a>WDDM 2.1 Cap

驱动程序将报告通过 WDDM 2.1 支持[DXGK_DRIVERCAPS::WDDMVersion](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)与新的版本常量：

`DXGK_WDDMVERSION::DXGKDDI_WDDMv2_1 = 0x2100`

将不会使用 Dxgkrnl **WDDMVersion**上限作为一种方法来确定支持哪些新功能 — 该任务将保留为其他大写字母或 DDI 是否存在。 但是，如果该驱动程序报告 WDDM 2.1 支持通过**WDDMVersion** dxgkrnl 大写字母或所需的 WDDM 2.1 DDIs 存在并且无法创建适配器，如果它们不会验证的上限。 不一致的上限将导致无法创建适配器或段。

> [!NOTE]
> 应用程序，现有或更高版本不能查询驱动程序模型，以充分利用任何 Windows 10 周年纪念版功能，这些通过平台改进，例如此处所述的那些启用的功能。 必须通过各自的运行时提供的任何功能更改。

添加了新常量，以匹配 KMT_DRIVERVERSION_WDDM_2_1:

```cpp
typedef enum _DXGIDRIVERMODELVERSION
{
    DXGIDMVERSION_1_0            = 1000,
    DXGIDMVERSION_1_1_PRERELEASE = 1102,
    DXGIDMVERSION_1_1            = 1105, 
    DXGIDMVERSION_1_2            = 1200,
    DXGIDMVERSION_1_3            = 1300,
    DXGIDMVERSION_2_0            = 2000,
    DXGIDMVERSION_2_1            = 2100,

} DXGIDRIVERMODELVERSION;
```

在 KMD DDI 接口版本如下所示： 

```cpp
#define DXGKDDI_INTERFACE_VERSION_VISTA      0x1052
#define DXGKDDI_INTERFACE_VERSION_VISTA_SP1  0x1053
#define DXGKDDI_INTERFACE_VERSION_WIN7       0x2005
#define DXGKDDI_INTERFACE_VERSION_WIN8       0x300E
#define DXGKDDI_INTERFACE_VERSION_WDDM1_3    0x4002
#define DXGKDDI_INTERFACE_VERSION_WDDM1_3_PATH_INDEPENDENT_ROTATION  0x4003
#define DXGKDDI_INTERFACE_VERSION_WDDM2_0    0x5023
#define DXGKDDI_INTERFACE_VERSION_WDDM2_1    0x6002
```

## <a name="graphics-inf-requirements"></a>图形 INF 要求

WDDM 2.1 图形驱动程序具有不同的 INF 要求相比 WDDM 2.0 或以前的驱动程序。 它们是：

1. WDDM 2.1 必须具有相同的功能评分的 WDDM 2.0 图形驱动程序 (D1)。

2. WDDM 2.1 图形驱动程序必须使用不同的 OS INF 安装部分。

3. WDDM 2.1 图形驱动程序 INF 更改为"驱动程序存储区"安装。

有关详细信息，请参阅[INF 文件的部分和指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)。

驱动程序文件，32 位和 64 位，将保留在中并从驱动程序存储区进行加载。 WoW64 文件系统重定向不适用于驱动程序存储区。 Ihv 可以使用标准 INF 语法来创建，例如，如果所需的唯一驱动程序存储区文件夹下的 WoW64 文件夹指定子文件夹。

下面是举例说明如何从驱动程序存储区中运行 INF 支持不同于以前的行为。

```inf
WINDOWS 10 ANNIVERSARY EDITION APPROACH: RUNNING DRIVERS FROM THE DRIVER STORE
[DestinationDirs]
KMDCopyFiles = 13
UMDCopyFiles = 13
UMDWoW64CopyFiles = 13

[DDInstall]
CopyFiles=KMDCopyFiles
CopyFiles=UMDCopyFiles
CopyFiles=UMDWoW64CopyFile

[KMDCopyFiles]
myKMD.sys

[UMDCopyFiles]
myUMD64.dll
myOpenCL64.dll
myOpenGL64.dll

[UMDWow64CopyFiles]
myUMD32.dll
myOpenCL32.dll
myOpenGL32.dll

[DDInstall.Services]
AddService = serviceName, 0x00000002, serviceName_Service_Inst

[serviceName_Service_Inst]
ServiceBinary = %13%\serviceName.sys

[regAdd]
HKR,,UserModeDriverName,%REG_MULTI_SZ%,%13%\myUMD64.dll, %13%\myUMD64.dll, %13%\myUMD64.dll, %13%\myUMD64.dll
HKR,,UserModeDriverNameWoW,%REG_MULTI_SZ%, %13%\myUMD32.dll, %13%\myUMD32.dll, %13%\myUMD32.dll, %13%\myUMD32.dll
HKLM,"Software\Khronos\OpenCL\Vendors",%13%\myOpenCL64.dll,%REG_DWORD%,0x00000000
HKLM,"Software\Wow6432Node\Khronos\OpenCL\Vendors",%13%\ myOpenCL32.dll,%REG_DWORD%,0x00000000
HKR,,OpenGLDriverName,%REG_MULTI_SZ%,%13%\myOpenGL64.dll
HKR,,OpenGLDriverNameWoW,%REG_MULTI_SZ%,%13%\myOpenGL32.dll
```

若要指定一个子文件夹，驱动程序可以使用语法，如下面的示例中所示：

```inf
...
[DestinationDirs]
...
UMDWoW64CopyFiles = 13,WoW64
...
[regAdd]
...
HRK,, UserModeDriverNameWoW,%REG_MULTI_SZ%, %13%\WoW64\myUMD.dll, %13%\WoW64\myUMD.dll, %13%\

The new manufacturer install section decoration for Windows 10 Anniversary edition WDDM 2.1 drivers is as follows: 
...
[Manufacturer]
%Grfx_Manf% =  IHVGfx, NTamd64.10.0…14310
...
[IHVGfx.NTamd64.10.0…14310]
; HW ID list
[list of HW IDs]
```

## <a name="driver-versioning"></a>驱动程序版本控制

图形适配器或芯片组的驱动程序 DLL 和 SYS 文件必须具有正确格式的文件版本。

驱动程序信息文件 (.inf)，必须与匹配内核模式驱动程序 (.sys) 和用户模式驱动程序 (.dll) 文件版本信息。 另外，在中发现的任何文件的版本信息`[SignatureAttributes]`部分作为二进制文件必须与匹配的 PETrust.inf。 inf。 建议在驱动程序包匹配的其他二进制文件的文件版本信息。 inf。

若要与旧操作系统的现行文件版本控制要求保持一致，文件版本格式必须按照`AA.BB.CCCCC.DDDDD`模式的位置：

* AA 指示最有能力的.inf 中列出的设备的驱动程序模型版本
* BB （对于 WDDM 1.2 驱动程序及更高版本）
    * 指示最支持的设备的.inf 中所列的最高可用 D3D 功能级别
* BB （WDDM 1.1 驱动程序及更低版本）
    * 指示最有能力的.inf 中列出的设备支持的最高可用 DDI 版本
* CCCCC 是最多 5 个数字 0 到 65535 选择由供应商的数字
* DDDDD 是最多 5 个数字 0 到 65535 选择由供应商的数字

AA 字段的值：

|驱动程序模型 |AA 值|
| --- | --- |
|WDDM v2.1 |21|
|WDDM v2.0 |20|
|WDDM v1.3 |10|
|WDDM v1.2 |9|
|WDDM v1.1|8|
|WDDM v1.0|7|
|XDDM|6|

BB 字段 (WDDM 1.2 及更高版本) 的值：

|DirectX 功能级别|BB 值|
|---|---|
12_x|21
12_1|20
12_0|19
11_1|18
11_0|17
10_1|16
10_0|15
9_3|14
9_2|14
9_1|14

BB 字段 (WDDM 1.1 及更早版本) 的值：

|DDI 版本|BB 值
---|---
在功能级别 11_0 D3D11-DDI|17
D3D11 DDI 10 的功能级别上|16
D3D10-DDI|15
D3D9 DDI|14

#### <a name="examples"></a>示例

> [!NOTE]
> 若要填充带前导零的数字不要求，即 123 不需要表示 00123 CCCCC 或 DDDDD 字段。 在以前版本的 Windows OS 的最后两个字段都是 4 位数字，即 CCCC。DDDD。 因此，对于 Windows 10 和 WDDM 2.0 之前的驱动程序版本的示例只需 4 位数字。

* Windows Vista WDDM 1.0:

    * D3D9 DDI 驱动程序可以使用 7.14.0000.0000 到 7.14.9999.9999
    * D3D10 DDI 驱动程序可以使用 7.15.0000.0000 到 7.15.9999.9999

* Windows 7 WDDM 1.1:

    * D3D9 DDI 驱动程序可以使用 8.14.0000.0000 到 8.14.9999.9999
    * D3D10 DDI 驱动程序可以使用 8.15.0000.0000 到 8.15.9999.9999
    * D3D11 DDI FL_10_0 驱动程序可以使用 8.16.0000.0000 到 8.16.9999.9999
    * D3D11 DDI FL_11_0 驱动程序可以使用 8.17.0000.0000 到 8.17.9999.9999

* Windows 8 WDDM 1.2:

    * FL_10_0 HW 可以使用 9.15.0000.0000 到 9.15.9999.9999
    * FL_10_1 HW 可以使用 9.16.0000.0000 到 9.16.9999.9999
    * FL_11_0 HW 可以使用 9.17.0000.0000 到 9.17.9999.9999
    * FL_11_1 HW 可以使用 9.18.0000.0000 到 9.18.9999.9999

* Windows 8.1 WDDM 1.3:

    * FL_10_0 HW 可以使用 10.15.0000.0000 到 10.15.9999.9999
    * FL_10_1 HW 可以使用 10.16.0000.0000 到 10.16.9999.9999
    * FL_11_0 HW 可以使用 10.17.0000.0000 到 10.17.9999.9999
    * FL_11_1 HW 可以使用 10.18.0000.0000 到 10.18.9999.9999

* Windows 10 WDDM 2.0:

    * FL_11_1 HW 可以使用 20.18.0000.0000 到 20.18.65535.65535
    * FL_12_0 HW 可以使用 20.19.0000.0000 到 20.19.65535.65535
    * FL_12_1 HW 可以使用 20.20.0000.0000 到 20.20.65535.65535

* Windows 10 WDDM 2.1:

    * FL_11_1 HW 可以使用 20.18.0000.0000 到 21.18.65535.65535
    * FL_12_0 HW 可以使用 20.19.0000.0000 到 21.19.65535.65535
    * FL_12_1 HW 可以使用 20.20.0000.0000 到 21.20.65535.65535


#### <a name="enforcement"></a>强制

高于 10586 将强制实施上述规则生成适用于 Windows 10 HLK 认证播放列表中的一个强制性测试。 测试将是可选的较旧操作系统版本。 对于 Windows 10 内部版本的 10586 WDDM 版本已更新到 2.1 后。 若要查看该文件的另一种方法是强制性要求仅适用于 WDDM 2.1 或更高版本生成的驱动程序。
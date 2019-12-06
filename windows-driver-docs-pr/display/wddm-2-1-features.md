---
title: WDDM 2.1 功能
description: 本部分提供有关 Windows 显示驱动程序模型（WDDM）版本2.1 中的新增功能和增强功能的详细信息。
ms.assetid: 7dc0d0ad-98da-4bd6-bed9-f70525b682bc
ms.date: 01/10/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4c579c6bfc9a3ded30a9212a828827b26adb3ef0
ms.sourcegitcommit: ba3199328ea5d80119eafc399dc989e11e7ae1d6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "74862972"
---
# <a name="wddm-21-features"></a>WDDM 2.1 功能


本主题提供有关 Windows 显示驱动程序模型（WDDM）版本2.1 中的新功能和增强功能的详细信息，可从 Windows 10 周年版开始。

WDDM 2.1 本身是可选的。 如果实现，则它是必需的和可选的驱动程序功能的集合。 任何支持这些功能的驱动程序都必须支持所有必需的功能。  可以通过 HLK 测试来验证支持，但 Dxgkrnl 将检查功能和 DDIs 中的一致性。

**WDDM 2.1 要求表**

| 功能 | 适用性 |
| --- | --- |
| 提供和回收改进 | Mandatory |
| 视频内存管理 | 可选 |
| 硬件保护的内容可靠性改进 | 选择硬件 |
| Windows GameDVR 的应用程序支持 | Mandatory |
| 间接显示 | 选择硬件 |
| 驱动程序存储区和并行安装 | Mandatory |
| 照相机/捕获方案的 DirectX 内存表面共享 | Mandatory|

WDDM 2.1 支持以下 D3D 版本： D3D9、D3D10、D3D 10.1、D3D11、D3D11、D3D12

## <a name="offer-and-reclaim-improvements"></a>提供和回收改进

为了减少后台模式下运行的应用程序的内存占用，创建了一个新的 DDI [PFND3DDDI_RECLAIMALLOCATIONS3CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimallocations3cb) 。 当进入后台时，此接口将使应用程序能够提供完全取消提交可接受的资源。 因此，进程生存期管理器将能够从使用 DirectX 的后台应用回收更多的内存，从而导致在内存压力下的后台应用程序终止更少。

其他 DDI 更改：

* [PFND3DDDI_UPDATEALLOCATIONPROPERTYCB 回调](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_updateallocationpropertycb)
* [PFND3DDDI_OFFERALLOCATIONS2CB 回调](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_offerallocations2cb)
* [D3DDDICB_OFFERALLOCATIONS2 结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddicb_offerallocations2)
* [D3DDDICB_RECLAIMALLOCATIONS3 结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_reclaimallocations3)

有关提供和回收资源的详细信息，请参阅[提供和回收更改](offer-and-reclaim-changes.md)。

## <a name="application-support-with-windows-gamedvr"></a>Windows GameDVR 的应用程序支持

Windows 10 周年纪念版包含使用 Windows 游戏栏和 GameDVR 全屏游戏的改进功能。

需要使用 WDDM 2.1 驱动程序来支持称为 "*现有批处理*" 的性能功能，这将为翻转模型交换链添加多线程支持。 这是一项重要的功能，可确保游戏栏的全屏游戏运行的性能与早期版本 Windows 的性能相同。

下表列出了为启用此功能而创建的新 DDIs：

* [PFND3DDDI_SYNCTOKENCB 回调](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_synctokencb)
* [D3DDDIARG_SYNCTOKEN 结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_synctoken)
* [PFND3DDDI_SYNCTOKEN 回调](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_synctoken)


## <a name="indirect-display"></a>间接显示

在 WDDM 2.1 中，间接显示允许 USB 连接的显示器与其他任何监视器的用户体验相同。 此外，间接显示驱动程序是一种用户模式驱动程序，它比使用内核模式驱动程序更简单，因而有助于提高整体系统可靠性。

在 WDDM 2.1 中，启用了以下 USB 显示功能/体验：

* 将 USB 显示连接到 Windows 平台或升级操作系统时，将从 Windows 更新下载并安装正确的驱动程序。

* 将监视器连接到 USB 显示硬件将检测并设置正确的监视器拓扑、分辨率和 DPI。

* 用户可以更改监视器的监视器分辨率和缩放。

* 用户可以断开 USB 显示，并重新连接显示器，而不会产生意外的副作用。

* 通过断开连接并重新连接到同一个监视器，监视拓扑。

* USB 显示工作正常，包括睡眠和休眠。

有关间接显示的详细信息，请参阅[间接显示驱动程序模型概述](indirect-display-driver-model-overview.md)

## <a name="driver-store-and-side-by-side-driver-installation"></a>驱动程序存储区和并行驱动程序安装

WDDM 2.1 介绍了如何通过*驱动程序存储区*安装图形驱动程序。 这种安装图形驱动程序的机制可以提高 Windows 更新的驱动程序更新的复原能力，消除驱动程序文件版本不匹配导致系统 instabilities 和用户启动的重新启动。 每个后续的驱动程序更新将直接从驱动程序存储区（即 `System32\DriverStore\FileRepository\[…]`）中的唯一位置运行，从而避免驱动程序文件覆盖和不匹配。

驱动程序存储区的功能实现需要更改图形驱动程序 INF 文件，以确保将驱动程序文件复制到唯一的驱动程序存储库中。 本文档的 " [Inf 要求](#graphics-inf-requirements)" 部分更详细地介绍了 inf 更改。

## <a name="dxil"></a>DXIL

WDDM 2.1 介绍如何将 GPU 着色器编译器堆栈从 DirectX 字节代码（DXBC）转换为 DirectX 中间语言（DXIL），这是一种用于将着色器指令传输到 GPU 的新格式。 过渡到 DXIL 为开发人员提供了以下好处：

* 通过最大限度地减少了开发人员熟悉的 GPU 编程语法和 CPU 语言之间的差异，简化了可编程性开发工作的简化和着色器创建过程的复杂性。

* 更高性能的编译器： 

    * 启用*运行时着色器性能*以提供改进的性能。 
    * DXIL 提供了一组新的内部函数，使你能够在 Gpu 中的 SIMD 处理器通道之间共享数据。

* 工作流灵活性-DXIL 使开发人员能够控制其自己的自定义工具和优化传递，并选择在生成时与运行时应用的编译步骤。

* 高级语言功能-演化语言提供的关键功能消除了 GPU 代码与 CPU 代码之间的差异，并为 GPU 程序员平展了学习曲线。

借助这些功能，重点介绍为开发人员带来的好处，最终用户即使在现有硬件上运行，最终用户也会看到更高性能的新的或更新的游戏的优势。

## <a name="directx-memory-surface-sharing-for-cameracapture-scenarios"></a>照相机/捕获方案的 DirectX 内存表面共享

在 WDDM 2.1 中，引入了框架服务器组件来跨多个进程同时共享照相机或捕获设备。 这样，便可以将捕获的帧保存到多个应用程序可从中读取的一个内存位置，而不是在进程之间复制图像数据，并多次复制进程。 此功能可以更高效地管理多个进程中的捕获图片、节能、为 WDDM 2.1 兼容硬件和驱动程序提供的延迟，从而提高应用程序和用户的性能。

框架服务器将捕获的映像作为交叉进程的可共享内存分配，并将此内存共享给请求访问的进程。 值得注意的是，由于框架服务器将纹理广播给多个客户端进程，纹理必须支持并发读取。 此目的目前支持 NV12 纹理。

## <a name="pipeline-state-object-pso-caching-and-library"></a>管道状态对象（PSO）缓存和库

管道状态对象（PSO）中引入了一个接口，该接口表示图形管道指令和资源（也称状态）作为统一对象，以减少 D3D 和状态的驱动程序分解之间的不匹配。 运行以图形方式苛刻的应用程序和游戏需要创建大量的 Pso。 

使用 WDDM 2.1 PSO 库和缓存，游戏应用程序可以在首次运行期间创建物理存储上的 PSO。 这使 D3D 运行时能够在以后的实例中从库中检索预先创建的 Pso，从而减少了 PSO 提取时间。 例如，在首次运行游戏后或重新启动 PC 后，内容将作为已保存的 Pso 从物理库中加载。


## <a name="start-of-pipeline-gpu-timestamps"></a>管道 GPU 时间戳的起始时间

在 WDDM 2.1 中，引入了在 GPU 管道中检索图形事件开始时间戳的功能。 这一新功能与管道时间戳的结束时间结合使用，为开发人员提供了对在 GPU 上发生的应用程序活动的并行化、流水线处理和计时的清晰且精细的可视化。 随着每个事件的执行时间的增加，开发人员可以进一步优化其代码，并调查低效和其他性能问题。

此功能有助于启用 "实时、低开销的 GPU 性能数据收集，同时提供足够的信息来可视化和测量 Gpu 上的工作负荷。 此功能的目的是提供足够的信息来重新构造 GPU 执行的操作的准确顺序和持续时间，以便工具可以直观显示并行，并处理引擎，测量 GPU 工作负荷，并识别潜在的同步问题。

## <a name="viewing-gpu-microcode"></a>查看 GPU 微代码

使用 WDDM 2.1，开发人员可通过提供 GPU 微码查看来进一步优化其着色。 开发人员通过在 HLSL 中创建着色器来编程图形管道，然后将其编译为 GPU 驱动程序的中间语言。 驱动程序运行其他编译和优化，以将此代码转换为对开发人员保持不透明的特定于 GPU 的指令。 利用此功能，开发人员可以阅读特定于 GPU 的代码，以评估其着色器优化和速度的程度。

此功能使 UMD 能够在图形管道的每个可编程阶段（也称为 着色器），并返回有关程序员使用或误用这些着色器的可操作信息。 GPU 特定的微代码会被反汇编，并显示为可读字符串格式以及 UMD 注释。 开发人员可以查看其 HLSL 代码映射，使其能够动态修改其代码，并在 GPU 代码端查看编译器优化结果。

## <a name="determining-wddm-version"></a>确定 WDDM 版本

### <a name="wddm-21-caps"></a>WDDM 2.1 Cap

驱动程序将使用新版本常量[DXGK_DRIVERCAPS：： WDDMVersion](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)报告 WDDM 2.1 支持：

`DXGK_WDDMVERSION::DXGKDDI_WDDMv2_1 = 0x2100`

Dxgkrnl 不会使用**WDDMVersion** cap 来确定受支持的新功能，而是将该任务保留为其他大写或 DDI 状态。 但是，如果驱动程序通过**WDDMVersion** CAP 报告 wddm 2.1 支持，dxgkrnl 将验证 wddm 2.1 所需的 Cap 或 DDIs 是否存在，如果不是，则无法创建适配器。 不一致的大写字母将导致创建适配器或段失败。

> [!NOTE]
> 应用程序（现有或较新）必须不需要查询驱动程序模型，才能利用通过平台改进（如此处所述的平台）启用的任何 Windows 10 周年纪念版功能。 必须通过各自的运行时显示任何功能更改。

添加了一个新常量，以匹配 KMT_DRIVERVERSION_WDDM_2_1：

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

KMD 中的 DDI 接口版本如下所示： 

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

与 WDDM 2.0 或以前的驱动程序相比，WDDM 2.1 图形驱动程序的 INF 要求不同。 它们是：

1. WDDM 2.1 必须具有与 WDDM 2.0 图形驱动程序（D1）相同的功能分数。

2. WDDM 2.1 图形驱动程序必须使用其他 OS INF 安装部分。

3. 用于 "驱动程序存储区" 安装的 WDDM 2.1 图形驱动程序 INF 发生了更改。

有关详细信息，请参阅[INF 文件部分和指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)。

驱动程序文件32和64位将保留在中，并从驱动程序存储区中加载。 WoW64 文件系统重定向不适用于驱动程序存储区。 例如，如果需要，Ihv 可以通过使用标准 INF 语法来指定子文件夹（例如，唯一的驱动程序存储文件夹下的 WoW64 文件夹）。

下面的示例演示了如何从驱动程序存储区中运行 INF 不同于以前的行为。

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

若要指定子文件夹，驱动程序可能使用语法，如以下示例中所示：

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

图形适配器或芯片集的驱动程序 DLL 和 SYS 文件必须具有格式正确的文件版本。

驱动程序信息文件（.inf）、内核模式驱动程序（.sys）和用户模式驱动程序（.dll）文件版本信息必须匹配。 此外，.inf 的 `[SignatureAttributes]` 部分中标识的任何文件的版本信息都必须与 .inf 匹配。 建议驱动程序包中其他二进制文件的文件版本信息与 .inf 匹配。

为了与旧版操作系统的访问文件版本控制要求保持一致，文件版本格式必须遵循 `AA.BB.CCCCC.DDDDD` 模式，其中：

* AA 指示 .inf 中列出的功能最强的设备的驱动程序型号版本
* BB （适用于 WDDM 1.2 驱动程序和更高版本）
    * 指示 .inf 中列出的功能最高的可用 D3D 功能级别。
* BB （适用于 WDDM 1.1 驱动程序和更低版本）
    * 指示 .inf 中列出的最受支持的设备支持的最高可用 DDI 版本
* AAAAA-BBBBB-CCCCC-DDDDDD-EEEEEE 是由供应商选择的0到65535之间的一个数字，最多5个数字
* DDDDD 是由供应商选择的0到65535之间的一个数字，最多5个数字

AA 字段的值：

|驱动程序型号 |AA 值|
| --- | --- |
|WDDM 2.1 版 |21|
|WDDM v2。0 |20|
|WDDM v1。0 |10|
|WDDM v2。0 |9|
|WDDM v1。1|8|
|WDDM v1。0|7|
|XDDM|6|

BB 字段的值（WDDM 1.2 及更高版本）：

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

BB 字段的值（WDDM 1.1 及更早版本）：

|DDI 版本|BB 值
---|---
D3D11-功能级别11_0 上的 DDI|17
D3D11-功能级别10上的 DDI|16
D3D10-DDI|15
D3D9 DDI|14

#### <a name="examples"></a>示例

> [!NOTE]
> 不需要用前导零填充数字，也就是说，123不需要为 AAAAA-BBBBB-CCCCC-DDDDDD-EEEEEE 或 DDDDD 字段表示为00123。 在以前版本的 Windows 操作系统中，最后两个字段的数量为4位，即 CCCC。DDDD. 因此，适用于 Windows 10 和 WDDM 2.0 之前的驱动程序版本的示例只有4位数。

* Windows Vista WDDM 1.0：

    * D3D9 DDI 驱动程序可以使用7.14.0000.0000 来7.14.9999.9999
    * D3D10 DDI 驱动程序可以使用7.15.0000.0000 来7.15.9999.9999

* Windows 7 WDDM 1.1：

    * D3D9 DDI 驱动程序可以使用8.14.0000.0000 来8.14.9999.9999
    * D3D10 DDI 驱动程序可以使用8.15.0000.0000 来8.15.9999.9999
    * 使用 FL_10_0 驱动程序的 D3D11 DDI 可以使用8.16.0000.0000 来8.16.9999.9999
    * 使用 FL_11_0 驱动程序的 D3D11 DDI 可以使用8.17.0000.0000 来8.17.9999.9999

* Windows 8 WDDM 1.2：

    * FL_10_0 硬件可以使用9.15.0000.0000 来9.15.9999.9999
    * FL_10_1 硬件可以使用9.16.0000.0000 来9.16.9999.9999
    * FL_11_0 硬件可以使用9.17.0000.0000 来9.17.9999.9999
    * FL_11_1 硬件可以使用9.18.0000.0000 来9.18.9999.9999

* Windows 8.1 WDDM 1.3：

    * FL_10_0 硬件可以使用10.15.0000.0000 来10.15.9999.9999
    * FL_10_1 硬件可以使用10.16.0000.0000 来10.16.9999.9999
    * FL_11_0 硬件可以使用10.17.0000.0000 来10.17.9999.9999
    * FL_11_1 硬件可以使用10.18.0000.0000 来10.18.9999.9999

* Windows 10 WDDM 2.0：

    * FL_11_1 硬件可以使用20.18.0000.0000 来20.18.65535.65535
    * FL_12_0 硬件可以使用20.19.0000.0000 来20.19.65535.65535
    * FL_12_1 硬件可以使用20.20.0000.0000 来20.20.65535.65535

* Windows 10 WDDM 2.1：

    * FL_11_1 硬件可以使用20.18.0000.0000 来21.18.65535.65535
    * FL_12_0 硬件可以使用20.19.0000.0000 来21.19.65535.65535
    * FL_12_1 硬件可以使用20.20.0000.0000 来21.20.65535.65535


#### <a name="enforcement"></a>强制性

适用于 Windows 10 10586 版本的 HLK 认证播放列表中的必需测试将强制实施上述规则。 对于较旧的操作系统版本，测试将是可选的。 对于 Windows 10 版本后10586，WDDM 版本已更新为2.1。 另一种查看方法是强制要求仅适用于为 WDDM 2.1 或更高版本生成的驱动程序。
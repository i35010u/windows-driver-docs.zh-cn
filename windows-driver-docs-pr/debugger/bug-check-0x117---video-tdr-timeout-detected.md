---
title: Bug 检查 0x117 VIDEO_TDR_TIMEOUT_DETECTED
description: VIDEO_TDR_TIMEOUT_DETECTED bug 检查具有 0x00000117 值。 这表示显示驱动程序无法及时响应。
ms.assetid: 70e24a97-f695-4d35-b52f-69dfddecd9b5
keywords:
- Bug 检查 0x117 VIDEO_TDR_TIMEOUT_DETECTED
- VIDEO_TDR_TIMEOUT_DETECTED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_TDR_TIMEOUT_DETECTED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c8f68a259e7d886a2a7bb7c7d169c980b5bceada
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67521095"
---
# <a name="bug-check-0x117-videotdrtimeoutdetected"></a>Bug 检查 0x117：VIDEO\_TDR\_TIMEOUT\_DETECTED


视频\_TDR\_超时\_检测到错误检查的值为 0x00000117。 这表示显示驱动程序无法及时响应。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="videotdrtimeoutdetected-parameters"></a>视频\_TDR\_超时\_检测到参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>指向内部 TDR 恢复情况下，如果可用的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>一个指针，到负责的设备驱动程序模块 （例如，所有者标记）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>辅助的特定于驱动程序的存储桶密钥。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>内部上下文相关数据，如果可用。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

图形中常见的稳定性问题发生时系统处理的最终用户命令或操作时出现完全冻结或挂起。 通常在 GPU 正忙于处理密集型的图形操作，通常在游戏过程。 无屏幕更新发生，并且用户假定他们的系统已被冻结。 用户通常等待几秒钟，并按电源按钮，然后重新启动系统。 Windows 会尝试检测这些有问题的情况下的挂起和动态恢复响应式桌面。

此检测和恢复的过程称为超时检测和恢复 (TDR)。 默认超时为 2 秒。 在视频卡 TDR 过程中，操作系统的 GPU 计划程序调用显示微型端口驱动程序[ *DxgkDdiResetFromTimeout* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)函数以重新初始化该驱动程序和重置 GPU。

如果恢复过程成功，将显示消息，指示的"显示驱动程序导致响应停止和已恢复。"

有关详细信息，请参阅超时检测和恢复 (TDR) [TDR 注册表项](https://docs.microsoft.com/windows-hardware/drivers/display/tdr-registry-keys)并[TDR 更改在 Windows 8 中的](https://docs.microsoft.com/windows-hardware/drivers/display/tdr-changes-in-windows-8)都位于[Windows 显示器驱动程序模型 （用于进行调试的提示WDDM)](https://docs.microsoft.com/windows-hardware/drivers/display/debugging-tips-for-the-windows-vista-display-driver-model)。

<a name="resolution"></a>分辨率
----------

GPU 花费的时间超过允许向您的监视器显示图形的多。 此行为可以发生的一个或多个原因如下：

-   您可能需要安装最新的更新的显示驱动程序，以便它正确支持 TDR 过程。
-   硬件问题的影响的视频卡能够正常工作，包括：
    -   超频的组件，如主板
    -   不正确的组件的兼容性和设置 （尤其是内存配置和执行时间）
    -   没有足够的系统冷却
    -   没有足够的系统电源
    -   有缺陷的部件 （如内存模块、 母板等）。
-   视觉效果或在后台运行的程序过多可能会拖慢您的 PC，以便根据需要视频卡无法响应。

[ **！ 分析**](-analyze.md)调试扩展显示有关错误检查的信息，有助于在确定根本原因。

```dbgcmd
3: kd> !analyze -v
*******************************************************************************
*                                                                             *
*                        Bugcheck Analysis                                    *
*                                                                             *
*******************************************************************************

VIDEO_TDR_TIMEOUT_DETECTED (117)
The display driver failed to respond in timely fashion.
(This code can never be used for a real bugcheck.)
Arguments:
Arg1: 8975d500, Optional pointer to internal TDR recovery context (TDR_RECOVERY_CONTEXT).
Arg2: 9a02381e, The pointer into responsible device driver module (e.g owner tag).
Arg3: 00000000, The secondary driver specific bucketing key.
Arg4: 00000000, Optional internal context dependent data.

...
```

此外显示将是出错的模块名称

```dbgcmd
MODULE_NAME: atikmpag

IMAGE_NAME:  atikmpag.sys
```

Lmv 命令可用于显示有关该错误的驱动程序，包括时间戳信息。

```dbgcmd
3: kd> lmvm atikmpag
Browse full module list
start    end        module name
9a01a000 9a09a000   atikmpag T (no symbols)           
    Loaded symbol image file: atikmpag.sys
    Image path: atikmpag.sys
    Image name: atikmpag.sys
    Browse all global symbols  functions  data
    Timestamp:        Fri Dec  6 12:20:32 2013 (52A23190)
    CheckSum:         0007E58A
    ImageSize:        00080000
    Translations:     0000.04b0 0000.04e4 0409.04b0 0409.04e4
```

参数 1 包含一个指向 TDR\_恢复\_上下文。

```dbgcmd
3: kd> dt dxgkrnl!_TDR_RECOVERY_CONTEXT fffffa8010041010
   +0x000 Signature        : ??
   +0x004 pState           : ???? 
   +0x008 TimeoutReason    : ??
   +0x010 Tick             : _ULARGE_INTEGER
   +0x018 pAdapter         : ???? 
   +0x01c pVidSchContext   : ???? 
   +0x020 GPUTimeoutData   : _TDR_RECOVERY_GPU_DATA
   +0x038 CrtcTimeoutData  : _TDR_RECOVERY_CONTEXT::<unnamed-type-CrtcTimeoutData>
   +0x040 DbgOwnerTag      : ??
   +0x048 PrivateDbgInfo   : _TDR_DEBUG_REPORT_PRIVATE_INFO
   +0xae0 pDbgReport       : ???? 
   +0xae4 pDbgBuffer       : ???? 
   +0xae8 DbgBufferSize    : ??
   +0xaec pDumpBufferHelper : ???? 
   +0xaf0 pDbgInfoExtension : ???? 
   +0xaf4 pDbgBufferUpdatePrivateInfo : ???? 
   +0xaf8 ReferenceCount   : ??
Memory read error 10041b08
```

参数 2 包含到负责的设备驱动程序模块 （例如，所有者标记） 的指针。

```dbgcmd
BUGCHECK_P2: ffffffff9a02381e
```

你可能想要检查堆栈跟踪使用[ **k、 kb、 kc、 kd、 kp、 kP，kv （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令。

```dbgcmd
3: kd> k
 # ChildEBP RetAddr  
00 81d9ace0 976e605e dxgkrnl!TdrUpdateDbgReport+0x93 [d:\blue_gdr\windows\core\dxkernel\dxgkrnl\core\dxgtdr.cxx @ 944]
01 81d9acfc 976ddead dxgkrnl!TdrCollectDbgInfoStage2+0x195 [d:\blue_gdr\windows\core\dxkernel\dxgkrnl\core\dxgtdr.cxx @ 1759]
02 81d9ad24 976e664f dxgkrnl!DXGADAPTER::Reset+0x23f [d:\blue_gdr\windows\core\dxkernel\dxgkrnl\core\adapter.cxx @ 14972]
03 81d9ad3c 977be9e0 dxgkrnl!TdrResetFromTimeout+0x16 [d:\blue_gdr\windows\core\dxkernel\dxgkrnl\core\dxgtdr.cxx @ 2465]
04 81d9ad50 977b7518 dxgmms1!VidSchiRecoverFromTDR+0x13 [d:\blue_gdr\windows\core\dxkernel\dxgkrnl\dxgmms1\vidsch\vidscher.cxx @ 1018]
05 (Inline) -------- dxgmms1!VidSchiRun_PriorityTable+0xfa71
06 81d9ad70 812c01d4 dxgmms1!VidSchiWorkerThread+0xfaf2 [d:\blue_gdr\windows\core\dxkernel\dxgkrnl\dxgmms1\vidsch\vidschi.cxx @ 424]
07 81d9adb0 81325fb1 nt!PspSystemThreadStartup+0x58 [d:\blue_gdr\minkernel\ntos\ps\psexec.c @ 5884]
08 81d9adbc 00000000 nt!KiThreadStartup+0x15 [d:\blue_gdr\minkernel\ntos\ke\i386\threadbg.asm @ 81]
```

此外可以导致此停止代码在代码中设置断点并单步前进到出错的代码中，如果可以一成不变地重现停止代码尝试。

有关详细信息，请参阅以下主题：

[故障转储分析使用 Windows 调试器 (WinDbg)](crash-dump-files.md)

如果您不准备使用 Windows 调试器处理此问题，可以使用一些基本的故障排除方法。

-   检查事件查看器中的系统日志可能有助于识别设备或驱动程序导致此错误检查的其他错误消息。

-   如果驱动程序标识在错误检查消息中，禁用该驱动程序或咨询驱动程序更新的制造商。

-   验证所有图形都相关的软件如 DirectX 和 OpenGL 是最新，并完全修补任何图形密集型应用程序 （如游戏）。
-   确认已安装任何新硬件与安装的 Windows 版本兼容。 例如，可以获取有关在所需的硬件信息[Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)。

-   **使用安全模式**

    请考虑使用安全模式下以帮助隔离此问题。 使用安全模式下加载的最小所需的驱动程序和系统服务在 Windows 启动过程。 若要进入安全模式下，使用**更新和安全**设置中。 选择**恢复**-&gt;**高级启动**启动到维护模式。 在生成菜单中选择**进行故障排除**- &gt; **高级选项** - &gt; **启动设置** - &gt; **重新启动**。 Windows 重新启动到后**启动设置**屏幕上，选择选项 4、 5 或 6 到安全模式下启动。

    安全模式下可通过按功能键上启动，例如 F8。 请参阅信息从制造商为特定的启动选项。

-   运行 Windows 内存诊断工具，用于测试的内存。 在控件面板的搜索框中，键入内存，然后单击**诊断您的计算机的内存问题**。在测试运行后，使用事件查看器查看系统日志下的结果。 寻找*MemoryDiagnostics 结果*条目以查看结果。

-   您可以尝试运行硬件诊断程序提供的系统制造商。

-   有关其他的常规疑难解答信息，请参阅[**蓝色屏幕数据**](blue-screen-data.md)。

<a name="remarks"></a>备注
-------

**硬件认证要求**

当它们实现 TDR 硬件设备必须满足的要求的信息，请参阅 WHCK 文档上*Device.Graphics...TDRResiliency*。

 

 





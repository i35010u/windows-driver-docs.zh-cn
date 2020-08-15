---
title: Bug 检查 0x117 VIDEO_TDR_TIMEOUT_DETECTED
description: VIDEO_TDR_TIMEOUT_DETECTED bug 检查的值为0x00000117。 这表示显示驱动程序未能及时响应。
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
ms.openlocfilehash: 84b4232f138258f4f9ce9dbd86382019753b6590
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88253097"
---
# <a name="bug-check-0x117-video_tdr_timeout_detected"></a>Bug 检查0x117： \_ \_ 检测到视频 TDR 超时 \_


\_检测到的视频 TDR \_ 超时 \_ bug 检查的值为0x00000117。 这表示显示驱动程序未能及时响应。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅 [排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="video_tdr_timeout_detected-parameters"></a>视频 \_ TDR \_ \_ 检测到超时参数


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
<td align="left"><p>指向内部 TDR 恢复上下文的指针（如果可用）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>指向 "负责的设备驱动程序" 模块 (例如，所有者标记) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>辅助驱动程序特定的存储桶键。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>内部上下文相关数据（如果有）。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

当系统在处理最终用户命令或操作时出现完全冻结或挂起时，图形中会出现常见的稳定性问题。 通常，GPU 是繁忙的处理密集型图形操作，通常在游戏播放期间。 不会进行屏幕更新，用户假定其系统已冻结。 用户通常会等待几秒钟，并按下 "电源" 按钮重新启动系统。 Windows 将尝试检测这些问题挂起情况并动态恢复响应式桌面。

此检测和恢复过程称为超时检测和恢复 (TDR) 。 默认超时为2秒。 在视频卡的 TDR 过程中，操作系统的 GPU 计划程序调用显示微型端口驱动程序的 [*DxgkDdiResetFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout) 函数来重新初始化驱动程序并重置 GPU。

如果恢复过程成功，将显示一条消息，指示 "显示驱动程序已停止响应并已恢复"。

有关详细信息，请参阅超时检测和恢复 (TDR) ，Windows 8 中的 [TDR 注册表项](https://docs.microsoft.com/windows-hardware/drivers/display/tdr-registry-keys) 和 [TDR 更改](https://docs.microsoft.com/windows-hardware/drivers/display/tdr-changes-in-windows-8) ，这些更改位于 [windows 显示驱动程序模型 (WDDM) 的调试提示 ](https://docs.microsoft.com/windows-hardware/drivers/display/debugging-tips-for-the-windows-vista-display-driver-model)中。

<a name="resolution"></a>解决方法
----------

GPU 比允许向监视器显示图形所用时间更长。 以下一种或多种原因可能会导致此行为：

-   可能需要安装最新的显示器驱动程序更新，以便正确支持 TDR 流程。
-   影响视频卡的功能正常运行的硬件问题，其中包括：
    -   超时钟组件，如主板
    -   错误的组件兼容性和设置 (特别是内存配置和计时) 
    -   系统冷却不足
    -   系统电量不足
    -   内存模块、主板等 (有缺陷的部件 ) 
-   视觉效果或在后台中运行的程序太多可能会减慢您的 PC 速度，使视频卡不能根据需要进行响应。

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。

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

还显示为错误模块名称

```dbgcmd
MODULE_NAME: atikmpag

IMAGE_NAME:  atikmpag.sys
```

可以使用 lmv 命令显示有关错误驱动程序的信息，包括时间戳。

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

参数1包含指向 TDR \_ 恢复上下文的指针 \_ 。

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

参数2包含指向负责的设备驱动程序模块的指针 (例如，所有者标记) 。

```dbgcmd
BUGCHECK_P2: ffffffff9a02381e
```

你可能希望使用 [**k、kb、glm-kc-qnw、kd、kp、kp、kv (显示 Stack Backtrace) **](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令来检查堆栈跟踪。

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

你还可以在代码中设置一个断点，使其导致此 stop 代码，并尝试单步前进到错误代码，前提是你能够持续重现停止代码。

有关详细信息，请参阅以下主题：

[使用 Windows 调试器 (WinDbg) 进行故障转储分析](crash-dump-files.md)

如果你不具备使用 Windows 调试器来处理此问题，则可以使用一些基本的故障排除技术。

-   查看事件查看器中的系统日志，以获取可能有助于识别导致此错误检查的设备或驱动程序的其他错误消息。

-   如果驱动程序标识在错误检查消息中，禁用该驱动程序或咨询驱动程序更新的制造商。

-   验证所有与图形相关的软件（例如 DirectX 和 OpenGL）是否是最新的，以及是否已对任何图形密集型应用程序 (如游戏) 进行了完全修补。
-   确认安装的任何新硬件都与安装的 Windows 版本兼容。 例如，可以在 [Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)中获取有关所需硬件的信息。

-   **使用安全模式**

    请考虑使用安全模式来帮助隔离此问题。 使用安全模式仅加载 Windows 启动过程中所需的最少驱动程序和系统服务。 若要进入安全模式，请使用 "设置" 中的 " **更新和安全** "。 选择 "**恢复** - &gt; **高级启动**" 以启动到维护模式。 在出现的菜单中，**选择 "** - &gt; **高级选项**" "启动  - &gt; **设置**  - &gt; **重新启动**"。 Windows 重启到 " **启动设置** " 屏幕后，选择 "选项"、"4"、"5" 或 "6" 以启动到安全模式。

    可以通过在启动时按功能键来提供安全模式，例如 F8。 请参阅制造商提供的有关特定启动选项的信息。

-   运行 Windows 内存诊断工具来测试内存。 在 "控制面板" 搜索框中键入 "内存"，然后选择 " **诊断计算机的内存问题**"。运行测试后，使用事件查看器查看系统日志下的结果。 查找 " *MemoryDiagnostics* " 项，查看结果。

-   你可以尝试运行系统制造商提供的硬件诊断。

-   有关其他常规疑难解答信息，请参阅 [**蓝屏数据**](blue-screen-data.md)。

<a name="remarks"></a>备注
-------

**硬件认证要求**

有关硬件设备实现 TDR 时必须满足的要求的信息，请参阅设备上的 WHCK 文档 *.。。TDRResiliency*。

 

 





---
title: Bug 检查 0x116 VIDEO_TDR_FAILURE
description: VIDEO_TDR_FAILURE bug 检查的值为0x00000116。 这表示试图重置显示驱动程序并从超时恢复失败。
ms.assetid: 06fe312a-e2d3-479f-b0fb-06c0ac79be32
keywords:
- Bug 检查 0x116 VIDEO_TDR_FAILURE
- VIDEO_TDR_FAILURE
- VIDEO_TDR_ERROR
ms.date: 01/17/2019
topic_type:
- apiref
api_name:
- VIDEO_TDR_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5833321ff9f4bfcf8170a28c5ab18cfde0f28996
ms.sourcegitcommit: 20eac54e419a594f7cea766ee28f158559dfd79c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91755020"
---
# <a name="bug-check-0x116-video_tdr_failure"></a>Bug 检查0x116：视频 \_ TDR \_ 失败


视频 \_ TDR \_ 失败 bug 检查的值为0x00000116。 这表示试图重置显示驱动程序并从超时恢复失败。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="video_tdr_failure-parameters"></a>视频 \_ TDR \_ 失败参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">说明</th>
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
<td align="left"><p>上次失败的操作的错误代码（如果可用）。</p></td>
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

此检测和恢复过程称为超时检测和恢复 (TDR) 。 默认超时为2秒。 在视频卡的 TDR 过程中，操作系统的 GPU 计划程序调用显示微型端口驱动程序的 [*DxgkDdiResetFromTimeout*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout) 函数来重新初始化驱动程序并重置 GPU。

在此过程中，操作系统会通知驱动程序不要访问硬件或内存，并为当前正在运行的线程提供一小段时间来完成。 如果线程未在超时内完成，系统 bug 将检查 0x116 VIDEO \_ TDR \_ 失败。 有关详细信息，请参阅 [线程同步和 TDR](../display/thread-synchronization-and-tdr.md)。

\_如果在很短的时间内出现大量 TDR 事件，系统还可能会错误地检查视频 TDR \_ 故障，这种情况下，在一分钟内默认超过五个 tdr。

如果恢复过程成功，将显示一条消息，指示 "显示驱动程序已停止响应并已恢复"。

有关详细信息，请参阅超时检测和恢复 (TDR) ，Windows 8 中的 [TDR 注册表项](../display/tdr-registry-keys.md) 和 [TDR 更改](../display/tdr-changes-in-windows-8.md) ，这些更改位于 [超时检测和恢复 (TDR) ](../display/timeout-detection-and-recovery.md)。

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
1: kd> !analyze -v
*******************************************************************************
*                                                                             *
*                        Bugcheck Analysis                                    *
*                                                                             *
*******************************************************************************

VIDEO_TDR_FAILURE (116)
Attempt to reset the display driver and recover from timeout failed.
Arguments:
Arg1: ffffe000c2c404c0, Optional pointer to internal TDR recovery context (TDR_RECOVERY_CONTEXT).
Arg2: fffff8016470c14c, The pointer into responsible device driver module (e.g. owner tag).
Arg3: ffffffffc000009a, Optional error code (NTSTATUS) of the last failed operation.
Arg4: 0000000000000004, Optional internal context dependent data.

...
```

还显示为错误模块名称

```dbgcmd
MODULE_NAME: nvlddmkm

IMAGE_NAME:  nvlddmkm.sys
```

您可以使用 " [**lm (List 已加载模块") **](lm--list-loaded-modules-.md)命令显示有关错误驱动程序的信息，包括时间戳。

```dbgcmd
1: kd> lmvm nvlddmkm
Browse full module list
start             end                 module name
fffff801`63ec0000 fffff801`649a7000   nvlddmkm T (no symbols)           
    Loaded symbol image file: nvlddmkm.sys
    Image path: \SystemRoot\system32\DRIVERS\nvlddmkm.sys
    Image name: nvlddmkm.sys
    Browse all global symbols  functions  data
    Timestamp:        Wed Jul  8 15:43:44 2015 (559DA7A0)
    CheckSum:         00AA7491
    ImageSize:        00AE7000
    Translations:     0000.04b0 0000.04e4 0409.04b0 0409.04e4
```

参数1包含指向 TDR \_ 恢复上下文的指针 \_ 。 如！分析输出中所示，如果有关联代码的符号，则可以使用 dt 命令来显示此数据。

```dbgcmd
1: kd> dt dxgkrnl!_TDR_RECOVERY_CONTEXT ffffe000c2c404c0
   +0x000 Signature        : 0x52445476
   +0x008 pState           : 0xffffe000`c2b12a40 ??
   +0x010 TimeoutReason    : 9 ( TdrEngineTimeoutPromotedToAdapterReset )
   +0x018 Tick             : _ULARGE_INTEGER 0xb2
   +0x020 pAdapter         : 0xffffe000`c2a89010 DXGADAPTER
   +0x028 pVidSchContext   : (null) 
   +0x030 GPUTimeoutData   : _TDR_RECOVERY_GPU_DATA
   +0x048 CrtcTimeoutData  : _TDR_RECOVERY_CONTEXT::<unnamed-type-CrtcTimeoutData>
   +0x050 pProcessName     : (null) 
   +0x058 DbgOwnerTag      : 0xfffff801`6470c14c
   +0x060 PrivateDbgInfo   : _TDR_DEBUG_REPORT_PRIVATE_INFO
   +0xb00 pDbgReport       : 0xffffe000`c2c3f750 _WD_DEBUG_REPORT
   +0xb08 pDbgBuffer       : 0xffffc000`bd000000 Void
   +0xb10 DbgBufferSize    : 0x37515
   +0xb18 pDumpBufferHelper : (null) 
   +0xb20 pDbgInfoExtension : 0xffffc000`ba7e47a0 _DXGKARG_COLLECTDBGINFO_EXT
   +0xb28 pDbgBufferUpdatePrivateInfo : 0xffffc000`bd000140 Void
   +0xb30 ReferenceCount   : 0n1
   +0xb38 pResetCompletedEvent : (null) 
```

参数2包含指向负责的设备驱动程序模块的指针 (例如，所有者标记) 。

```dbgcmd
1: kd> ub fffff8016470c14c
nvlddmkm+0x84c132:
fffff801`6470c132 cc              int     3
fffff801`6470c133 cc              int     3
fffff801`6470c134 48ff254d2deaff  jmp     qword ptr [nvlddmkm+0x6eee88 (fffff801`645aee88)]
fffff801`6470c13b cc              int     3
fffff801`6470c13c 48ff252d2eeaff  jmp     qword ptr [nvlddmkm+0x6eef70 (fffff801`645aef70)]
fffff801`6470c143 cc              int     3
fffff801`6470c144 48ff257d2deaff  jmp     qword ptr [nvlddmkm+0x6eeec8 (fffff801`645aeec8)]
fffff801`6470c14b cc              int     3
```

你可能希望使用 [**k、kb、glm-kc-qnw、kd、kp、kp、kv (显示 Stack Backtrace) **](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令来检查堆栈跟踪。

```dbgcmd
1: kd> k
 # Child-SP          RetAddr           Call Site
00 ffffd001`7d53d918 fffff801`61ba2b4c nt!KeBugCheckEx [d:\th\minkernel\ntos\ke\amd64\procstat.asm @ 122]
01 ffffd001`7d53d920 fffff801`61b8da0e dxgkrnl!TdrBugcheckOnTimeout+0xec [d:\th\windows\core\dxkernel\dxgkrnl\core\dxgtdr.cxx @ 2731]
02 ffffd001`7d53d960 fffff801`61b8dd7f dxgkrnl!ADAPTER_RENDER::Reset+0x15e [d:\th\windows\core\dxkernel\dxgkrnl\core\adapter.cxx @ 19443]
03 ffffd001`7d53d990 fffff801`61ba2385 dxgkrnl!DXGADAPTER::Reset+0x177 [d:\th\windows\core\dxkernel\dxgkrnl\core\adapter.cxx @ 19316]
04 ffffd001`7d53d9e0 fffff801`63c5fba7 dxgkrnl!TdrResetFromTimeout+0x15 [d:\th\windows\core\dxkernel\dxgkrnl\core\dxgtdr.cxx @ 2554]
05 ffffd001`7d53da10 fffff801`63c47e5d dxgmms1!VidSchiRecoverFromTDR+0x11b [d:\th\windows\core\dxkernel\dxgkrnl\dxgmms1\vidsch\vidscher.cxx @ 1055]
06 ffffd001`7d53dbc0 fffff801`aa55c698 dxgmms1!VidSchiWorkerThread+0x8d [d:\th\windows\core\dxkernel\dxgkrnl\dxgmms1\vidsch\vidschi.cxx @ 426]
07 ffffd001`7d53dc00 fffff801`aa5c9306 nt!PspSystemThreadStartup+0x58 [d:\th\minkernel\ntos\ps\psexec.c @ 6845]
08 ffffd001`7d53dc60 00000000`00000000 nt!KxStartSystemThread+0x16 [d:\th\minkernel\ntos\ke\amd64\threadbg.asm @ 80]
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

-   运行 Windows 内存诊断工具来测试内存。 在 "控制面板" 搜索框中键入 "内存"，然后选择 " **诊断计算机的内存问题**"。运行测试后，使用事件查看器查看系统日志下的结果。 查找“内存诊断结果”条目以查看结果  。

-   你可以尝试运行系统制造商提供的硬件诊断。

-   有关其他常规疑难解答信息，请参阅 [**蓝屏数据**](blue-screen-data.md)。

<a name="remarks"></a>备注
-------

**硬件认证要求**

有关硬件设备实现 TDR 时必须满足的要求的信息，请参阅设备上的 WHCK 文档 *.。。TDRResiliency*。
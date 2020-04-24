---
title: 音频度量
description: 音频度量定义
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 91afcac656d5be6fba78b8b1b61df1e4dd6394e3
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "74860817"
---
# <a name="audio-measures"></a>音频度量

## <a name="audio-stream-initialization"></a>音频流初始化

每当应用程序（或 Windows 组件）需要播放或录制音频时，它都会使用多种音频 API 中的一种。

所有音频 API 最终都调用核心音频 API 调用 [IAudioClient::Initialize](https://docs.microsoft.com/windows/win32/api/audioclient/nf-audioclient-iaudioclient-initialize)。 这会在应用程序和 Windows 音频引擎之间建立连接，并在 Windows 音频引擎与音频驱动程序之间建立连接。

如果 IAudioClient::Initialize 调用失败，则应用程序将无法使用音频，但有一些例外。 有些 IAudioClient::Initialize 错误是良性的，将被忽略；[附录](measure-appendix.md)中提供了这些错误的列表。

该调用的结果记录在 **Microsoft.Windows.Audio.Client** 提供程序的 **AudioClientInitialize** 遥测事件中。 如果调用成功，则 **HResult** 字段为 0；如果调用失败，则该字段为负数。

以下音频度量跟踪 IAudioClient::Initialize 成功情况：
* [至少有一次音频流初始化失败的计算机的百分比](pct-machines-with-at-least-one-audio-stream-initialization-failure.md)
* [流初始化成功率低于标准成功率的计算机的百分比](pct-machines-with-subpar-stream-initialization-success-rate.md)

## <a name="audio-user-mode-reliability"></a>音频用户模式可靠性

内核流音频驱动程序在内核模式下运行。 如果音频驱动程序发生异常，将导致蓝屏死机 (BSOD) 或绿屏死机 (GSOD)。

对于音频内核模式可靠性问题，没有专用的度量，但通常有针对内核模式可靠性问题的度量。

Windows 共享模式音频引擎在用户模式下运行。 具体而言，“Windows 音频”服务 AudioSrv.dll (AudioSrv) 在专用的 svchost.exe 进程中运行。 它还启动一个帮助程序“Windows 音频设备图形隔离”进程 audiodg.exe (AudioDg)。

音频 IHV 可以将插件包含到称为音频处理对象 (APO) 的用户模式音频引擎中。

如果 APO 发生异常，不会出现蓝屏死机，但 Windows 音频引擎会崩溃。 还有一个监视程序计时器，用于验证来自应用程序的调用是否在快速完成。 如果调用停滞，监视程序会注意到此情况，并强制 Windows 音频引擎崩溃。

无论采用哪种方式，系统上的所有音频都将丢失，直到音频引擎重新启动。

如果 AudioDg 崩溃并且 AudioSrv 注意到此情况，则会从 **Microsoft.Windows.Audio.Service** 提供程序记录一个 **AudioDgCrash** 遥测事件。 （在某些较早版本的 Windows 10 中，该事件为 **AudioDg-Crash**。）

如果 AudioSrv 崩溃并且 AudioDg 注意到此情况，则会从 **Microsoft.Windows.Audio.DeviceGraph** 提供程序记录一个 **AudioSrvSvchostCrash** 遥测事件。 （在某些较早版本的 Windows 10 中，该事件为 **AudioSrv-Svchost-Crash**。）

如果音频服务挂起，则会从 **Microsoft.Windows.Audio.Service** 提供程序中记录一个 **Hang** 遥测事件。 （在某些较早版本的 Windows 10 中，对于某些类型的挂起，还将从 **Microsoft.Windows.Audio.DeviceGraph** 提供程序中记录一个 **Hang** 事件。）

以下音频度量跟踪 Windows 音频引擎的可靠性：
* [至少有一次音频崩溃的计算机的百分比](percent-machines-with-at-least-one-audio-crash.md)
* [至少有一次音频挂起的计算机的百分比](pct-machines-with-at-least-one-audio-hang.md)

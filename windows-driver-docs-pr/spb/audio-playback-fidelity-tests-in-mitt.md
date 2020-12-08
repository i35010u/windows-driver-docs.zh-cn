---
title: MITT 中的音频播放保真度测试
description: MITT 板上的音频模块用于检测在音频设备传输级别发生的错误，方法是检测正弦波频率准确性 (零交叉) 并统计频率或偏移量不正确的实例。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3f8772d55c6f08669325b12f2fc1144dfb0a8e0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811855"
---
# <a name="audio-playback-fidelity-tests-in-mitt"></a>MITT 中的音频播放保真度测试

MITT 板上的音频模块用于检测在音频设备传输级别发生的错误，方法是检测正弦波频率准确性 (零交叉) 并统计频率或偏移量不正确的实例。 缺少信号或丢失的数据包将导致移动波形，这种波形可通过此机制自动听到和检测。

## <a name="before-you-begin"></a>在开始之前

- 获取 MITT 板和音频适配器。 请参阅 [购买使用 MITT 的硬件](./multi-interface-test-tool--mitt--.md)。
- [下载 MITT](/previous-versions/dn919810(v=vs.85))软件包。 在受测系统上安装它。
- 在 MITT 板上安装 MITT 固件。 请参阅 [MITT 入门](./get-started-with-mitt---.md)。

## <a name="hardware-setup"></a>硬件设置

![mitt 音频测试硬件设置](images/mitttoaudio.jpg)

1. 将音频适配器连接到 MITT 板上的 **JC1** 。
2. LineIn 通过使用 1/8 "至 1/8" 男连接到插头，从正在测试的系统上的音频设备中取出来自音频设备的输入。 其他音频源可能连接了相应的电缆。

## <a name="audio-playback-automation-tests"></a>音频播放自动化测试

1. 在要测试的系统上创建一个文件夹。
2. 将 AudiounitsimpleIO.dll 从 MITT 软件包复制到文件夹。
3. 使用此命令运行所有测试：

    te.exe audiounitSimpleIO.dll

4. 作为简单的 IO 插件运行，请使用包含的脚本 SimpleIO \_ MITT \_ Audio \_Sample.vbs
5. 若要禁用正在运行的音频 SimpleIO 测试，请设置以下注册表项：

**HKEY \_当前 \_ 用户 \\ 软件 \\ Microsoft \\ MITT \\ AudioUnit** * * * * * * \\ = RunAudioTest

数据类型  
REG \_ DWORD

描述  
设置为0。

这将从500hz 到18khz 播放一系列测试音，并报告检测到的故障数。 如果检测到大量故障（如 10000 +），请确认电缆已正确连接，并且音量未静音。 检测到任何中断的信号，并且每个预期交叉都有故障，因此数字可能非常高。

如果所有测试均通过，则设备已正确连接并按预期方式运行。

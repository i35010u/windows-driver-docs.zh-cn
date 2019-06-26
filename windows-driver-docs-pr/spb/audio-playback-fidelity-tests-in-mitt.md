---
title: MITT 中的音频播放保真度测试
description: MITT 板上的音频模块用于通过检测正弦波频率准确性 （在零叉号），然后计算频率或偏移量不正确的实例来检测在音频设备的传输级别发生的错误。
ms.assetid: 1EAAF6F7-17B6-452F-9273-D7CD1DC33154
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a1acb86e466cc1f68e7db4f0ad7a0db966870f9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369583"
---
# <a name="audio-playback-fidelity-tests-in-mitt"></a>MITT 中的音频播放保真度测试


**上次更新时间**

-   2015 年 1 月

**适用于：**

-   Windows 8.1

MITT 板上的音频模块用于通过检测正弦波频率准确性 （在零叉号），然后计算频率或偏移量不正确的实例来检测在音频设备的传输级别发生的错误。 缺少信号或丢失的数据包会导致移动波形声音且可通过此机制自动检测。

## <a name="before-you-begin"></a>开始之前...


-   获取 MITT 主板和音频的适配器。 请参阅[购买硬件使用 MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/multi-interface-test-tool--mitt--)。
-   [下载 MITT 软件包](https://docs.microsoft.com/previous-versions/dn919810(v=vs.85))。 待测试系统上安装它。
-   安装 MITT 固件 MITT 板上。 请参阅[开始使用 MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/get-started-with-mitt---)。

## <a name="hardware-setup"></a>硬件安装


![mitt 音频测试硬件安装](images/mitttoaudio.jpg)

1.  连接到声卡**JC1** MITT 板上。
2.  线路输入已从行无法音频设备输入待测试系统上使用到 1/8"male 到男性电缆 1/8"。 其他音频源可能具有适当的电缆连接设置。

## <a name="audio-playback-automation-tests"></a>音频播放自动化测试


1.  待测试系统上创建一个文件夹。
2.  MITT 软件程序包的 AudiounitsimpleIO.dll 复制到的文件夹中。
3.  使用此命令运行所有测试：

    te.exe audiounitSimpleIO.dll

4.  作为简单 IO 插件运行，请使用包含的脚本 SimpleIO\_MITT\_音频\_Sample.vbs
5.  若要禁用音频 SimpleIO 测试运行，请设置以下注册表项：
    -   **HKEY\_CURRENT\_USER\\Software\\Microsoft\\MITT\\AudioUnit** \\**** = RunAudioTest

           数据类型  
           REG\_DWORD

           描述  
           设置为 0。

这将播放一系列测试音，500 hz 至 18 khz 和报表中检测到的问题数。 如果检测到大量的问题，如 10000 +，则验证将电缆连接正确，不静音。 每个预期跨数量可能会非常高，因此故障检测到任何中断的信号。

如果所有测试都通过，设备已正确连接，并按预期操作。

 

 





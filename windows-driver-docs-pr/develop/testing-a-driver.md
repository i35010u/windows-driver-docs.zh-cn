---
ms.assetid: bb73768e-0ac9-4377-9caa-c0cce1d10bb8
title: 测试驱动程序
description: 测试驱动程序
ms.date: 06/28/2018
ms.localizationpriority: medium
ms.openlocfilehash: 53fa185c23d5d2b7c3f99e74d27482ff065f4d2c
ms.sourcegitcommit: 46654c090f937923d9712de114fdebe7deffeaaf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427687"
---
# <a name="testing-a-driver"></a>测试驱动程序

WDK 向 Visual Studio 添加驱动程序测试接口，可让你在网络中的远程测试计算机上生成、部署、安装和测试驱动程序。 WDK 还提供一系列设备驱动程序测试，你可以用来测试驱动程序的特性和功能。 你还可以在 Visual Studio 中使用驱动程序测试模板自定义或编写自己的驱动程序测试。

## <a name="span-idvideo_demonstrationspanspan-idvideo_demonstrationspanspan-idvideo_demonstrationspanvideo-demonstration"></a><span id="Video_Demonstration"></span><span id="video_demonstration"></span><span id="VIDEO_DEMONSTRATION"></span>视频演示


此视频演示如何在测试组中运行驱动程序相关测试。

<iframe class="video-iframe" style="width: 100%; height: 550px;" frameborder="0" allowfullscreen="true" src ="https://www.microsoft.com/videoplayer/embed/e12e5ce5-b41f-4b91-ab5f-69598ccdcb57?autoplay=false"></iframe> 

本部分介绍测试驱动程序的一些策略，以及有关如何选择和配置用于测试的远程计算机的信息。

若要准备将公开分发的驱动程序，应运行 [Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893)。 有关 Windows 认证计划以及如何获取 HCK 的信息，请参阅 [Windows 硬件认证计划](https://go.microsoft.com/fwlink/p/?linkid=227016)。

WDK 提供的测试二进制文件和工具支持轻松地从命令行运行设备基础功能测试。
有关详细信息，请参阅[通过命令行运行 DevFund 测试](https://review.docs.microsoft.com/windows-hardware/drivers/devtest/run-devfund-tests-via-the-command-line)。

## 
<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="strategies-for-testing-drivers-during-development.md" data-raw-source="[Tips for testing drivers during development](strategies-for-testing-drivers-during-development.md)">开发期间测试驱动程序的相关技巧</a></p></td>
<td align="left"><p><strong>应在何时开始测试？</strong> 了解驱动程序的要求后，便可以立即开始设计测试用例来测试是否已实现了这些关键要求。 研究表明，缺陷在代码中存在得越久，找到并修复这些缺陷就变得越代价高昂。 在开发周期的早期找到并修复缺陷，比在代码发布和分发之后查找缺陷成本更低、中断更少。 尽早创建测试用例还可以帮助你找出设计中存在的问题。</p>
<p></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="testing-a-driver-at-runtime.md" data-raw-source="[How to test a driver at runtime using Visual Studio](testing-a-driver-at-runtime.md)">如何使用 Visual Studio 在运行时测试驱动程序</a></p></td>
<td align="left"><p>Visual Studio 的 WDK 扩展提供设备测试接口，可让你在网络中的测试计算机上方便地生成、部署、安装和测试驱动程序。 WDK 提供一系列设备驱动程序测试，你可以用来测试驱动程序的特性和功能。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="how-to-write-a-driver-test-.md" data-raw-source="[How to write a driver test using a Driver Test template](how-to-write-a-driver-test-.md)">如何使用“驱动程序测试”模板编写驱动程序测试</a></p></td>
<td align="left"><p>你可以使用适用于 Windows 8 的 Windows 驱动程序工具包 (WDK) 来创建自己的驱动程序测试或自定义所提供的部分测试。 你可以使用 WDK 为 Microsoft Visual Studio Ultimate 2012 提供的驱动程序测试框架将你创建的测试部署到远程测试计算机。</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[用于验证驱动程序的工具](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-verifying-drivers)

 






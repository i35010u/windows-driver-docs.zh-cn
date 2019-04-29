---
title: 流媒体示例
description: 流媒体示例
ms.assetid: 797763a6-cd13-4d76-8ddb-75d812a8dde3
keywords:
- 流式处理媒体示例 WDK
- 示例 WDK 流式处理媒体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f559224f9dcd5b2d2097eb01ab355bdf3fda4b72
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359633"
---
# <a name="streaming-media-samples"></a>流媒体示例


### <a href="" id="streaming-media-samples"></a>

从 Windows 10 开始，GitHub 上提供了 [Windows 驱动程序示例存储库](https://go.microsoft.com/fwlink/p/?LinkId=616507)。

[Windows 8 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616509)并[Windows 8.1 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=618052)可以从下载[Windows 硬件开发人员中心](https://go.microsoft.com/fwlink/p/?LinkId=616506)。

在 Windows 7 中，Windows Driver Kit (WDK) 中包含示例。

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th>示例名称</th>
<th>构建环境</th>
<th>目标操作系统</th>
<th>即插即用驱动程序</th>
<th>在现成驱动程序</th>
<th>示例说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AVStream 筛选器为中心的模拟捕获驱动程序 (Avssamp)</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>筛选器为中心的 AVStream 捕获驱动程序提供功能的音频。 该驱动程序执行播放用户提供 pulse 代码调制 (PCM) 波形音频文件在循环中的时 RGB24 或 YUV422 格式 320 x 240 分辨率捕获。 此示例演示如何编写筛选器为中心的 AVStream 微型驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>AVStream 模拟的硬件示例驱动程序 (Avshws)</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>Pin 为中心的 AVStream 捕获驱动程序用于模拟的硬件。 该驱动程序执行的捕获是 320 x 240 个通过直接 DMA RGB24 或 YUV422 格式到捕获缓冲区。</p>
<p>本示例的目的是演示如何编写 pin 为中心的 AVStream 微型驱动程序。 该示例还演示如何通过使用 AVStream 提供的相关的功能来实现 DMA。</p>
<p>此示例功能增强了参数验证和溢出检测。</p></td>
</tr>
<tr class="odd">
<td><p>SonyDCam 1394 网络摄像头驱动程序</p></td>
<td><p>Windows 7</p></td>
<td><p>Windows 7</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>Microsoft Windows 驱动程序模型 (WDM) Stream 类视频捕获驱动程序支持基于 1394年的数字照相机的 1394年贸易协会从符合数字照相机规范。</p></td>
</tr>
<tr class="even">
<td><p>USBIntel 网络摄像头驱动程序</p></td>
<td><p>Windows 7</p></td>
<td><p>Windows 7</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>Microsoft Windows 驱动程序模型 (WDM) 流类视频捕获驱动程序。</p></td>
</tr>
<tr class="odd">
<td><p>软件调谐器</p></td>
<td><p>Windows 7</p></td>
<td><p>Windows 7</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>演示几个数字的网络类型。</p></td>
</tr>
</tbody>
</table>

 

 

 





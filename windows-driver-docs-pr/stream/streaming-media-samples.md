---
title: 流媒体示例
description: 流媒体示例
ms.assetid: 797763a6-cd13-4d76-8ddb-75d812a8dde3
keywords:
- 流式处理媒体示例 WDK
- 采样 WDK 流式处理媒体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ee41e9db592c07eca31e21706c7785f2262f900
ms.sourcegitcommit: eb1f58d23da3b1240385c072837d9118239a8f97
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2020
ms.locfileid: "75883892"
---
# <a name="streaming-media-samples"></a>流媒体示例

可以在[“Microsoft 示例”门户](https://docs.microsoft.com/samples/browse/?products=windows-wdk)上浏览和下载各个 Windows 10 驱动程序示例。 还可以在 GitHub 上克隆、分叉或下载 [Windows-driver-samples](https://github.com/Microsoft/Windows-driver-samples) 存储库。

Windows 驱动程序示例的早期版本存档在这里：

- [Windows 8.1 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=618052)

- [Windows 8 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616509)

对于 Windows 7，示例已包含在 Windows 驱动程序工具包 (WDK) 中。

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
<th>生成环境</th>
<th>目标操作系统</th>
<th>PnP 驱动程序</th>
<th>内置驱动程序</th>
<th>示例说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AVStream 以筛选器为中心的模拟捕获驱动程序（Avssamp）</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p></td>
<td><p>无</p></td>
<td><p>无</p></td>
<td><p>提供具有功能音频的以筛选为中心的 AVStream 捕获驱动程序。 在循环中播放用户提供的脉冲代码调制（PCM）波形音频文件时，驱动程序以 RGB24 或 YUV422 格式以 320 x 240 分辨率进行捕获。 此示例演示如何编写以筛选为中心的 AVStream 微型驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>AVStream 模拟硬件示例驱动程序（Avshws）</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p></td>
<td><p>无</p></td>
<td><p>无</p></td>
<td><p>为模拟的硬件部分提供以 pin 为中心的 AVStream 捕获驱动程序。 驱动程序在 320 x 240 上通过直接 DMA 到捕获缓冲区中的 RGB24 或 YUV422 格式执行捕获。</p>
<p>示例的目的是演示如何编写以 pin 为中心的 AVStream 微型驱动程序。 该示例还演示了如何使用 AVStream 提供的相关功能实现 DMA。</p>
<p>此示例的功能增强了参数验证和溢出检测。</p></td>
</tr>
<tr class="odd">
<td><p>SonyDCam 1394 网络摄像机驱动程序</p></td>
<td><p>Windows 7</p></td>
<td><p>Windows 7</p></td>
<td><p>无</p></td>
<td><p>“是”</p></td>
<td><p>一种 Microsoft Windows 驱动模型（WDM）流类视频捕获驱动程序，该驱动程序支持基于1394的数字照相机，该驱动程序符合1394贸易关联中的数字照相机规范。</p></td>
</tr>
<tr class="even">
<td><p>USBIntel 网络摄像机驱动程序</p></td>
<td><p>Windows 7</p></td>
<td><p>Windows 7</p></td>
<td><p>无</p></td>
<td><p>“是”</p></td>
<td><p>Microsoft Windows 驱动模型（WDM）流类视频捕获驱动程序。</p></td>
</tr>
<tr class="odd">
<td><p>软件调谐器</p></td>
<td><p>Windows 7</p></td>
<td><p>Windows 7</p></td>
<td><p>无</p></td>
<td><p>无</p></td>
<td><p>演示了几种数字网络类型。</p></td>
</tr>
</tbody>
</table>

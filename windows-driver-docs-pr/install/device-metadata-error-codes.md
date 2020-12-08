---
title: 设备元数据错误代码
description: 设备元数据错误代码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddb1e9a66c38f22219136393789725dcf825f3d7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782851"
---
# <a name="device-metadata-error-codes"></a>设备元数据错误代码


从 Windows 7 开始，操作系统会在与设备元数据包的下载和处理相关的事件内记录以下错误代码。 这些事件由 Windows (ETW) 服务的事件跟踪进行管理，可以使用事件查看器进行查看。 有关这些事件的详细信息，请参阅 [使用事件查看器调试设备元数据包](debugging-device-metadata-packages-by-using-event-viewer.md)。

<a href="" id="windows-metadata-and-internet-services--wmis--errors--200000xx-"></a>Windows 元数据和 Internet 服务 (WMIS) 错误 (200000xx)   
<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">错误代码</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>20000021</p></td>
<td align="left"><p>请求不包含设备元数据请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p>20000022</p></td>
<td align="left"><p>请求批大小超过了允许的最大值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>20000023</p></td>
<td align="left"><p>区域设置值无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>20000024</p></td>
<td align="left"><p>请求不包含有效的标头信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>20000025</p></td>
<td align="left"><p>请求格式无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>20000031</p></td>
<td align="left"><p>处理请求时服务端出现错误。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="device-metadata-retrieval-client--dmrc--errors--0x400000xx-"></a>设备元数据检索客户端 (DMRC) 错误 (0x400000xx)   
<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">错误代码</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>40000011</p></td>
<td align="left"><p>没有本地元数据缓存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>40000012</p></td>
<td align="left"><p>本地元数据缓存中) 的 (文件夹结构不正确。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>40000021</p></td>
<td align="left"><p>没有本地元数据存储。</p></td>
</tr>
<tr class="even">
<td align="left"><p>40000022</p></td>
<td align="left"><p>本地元数据存储区中)  (文件夹结构已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>40000031</p></td>
<td align="left"><p>DMRC 索引数据缺失。</p></td>
</tr>
<tr class="even">
<td align="left"><p>40000032</p></td>
<td align="left"><p>DMRC 索引数据已损坏。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="device-metadata-package-errors--0x500000xx-"></a> (0x500000xx) 的设备元数据包错误  
<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">错误代码</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>50000011</p></td>
<td align="left"><p><em>Devicemetadata</em> cabinet (<em>cab</em>) 文件已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>50000012</p></td>
<td align="left"><p><em>Devicemetadata-ms</em> cab 文件没有正确的设备元数据结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>50000021</p></td>
<td align="left"><p>缺少<em>PackageInfo.xml</em> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>50000022</p></td>
<td align="left"><p><em>PackageInfo.xml</em> 的格式不正确，无法对其进行分析。</p>
<div class="alert">
<strong>注意</strong>   此错误代码包括 <em>PackageInfo.xml</em> 文档缺少必需的元素，或者它的一个或多个元素基于 <a href="/previous-versions/windows/hardware/metadata/ff549614(v=vs.85)" data-raw-source="[PackageInfo XML Schema](/previous-versions/windows/hardware/metadata/ff549614(v=vs.85))">PackageInfo XML 架构</a>的语法无效。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td align="left"><p>50000031</p></td>
<td align="left"><p>缺少<em>DeviceInfo.xml</em> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>50000032</p></td>
<td align="left"><p><em>DeviceInfo.xml</em> 的格式不正确，无法对其进行分析。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>50000033</p></td>
<td align="left"><p><em>DeviceInfo.xml</em> 缺少必需的元素。</p></td>
</tr>
<tr class="even">
<td align="left"><p>50000034</p></td>
<td align="left"><p>根据 XML 架构定义， <em>DeviceInfo.xml</em> 中的元素无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>50000041</p></td>
<td align="left"><p>缺少<em>WindowsInfo.xml</em> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>50000042</p></td>
<td align="left"><p><em>WindowsInfo.xml</em> 的格式不正确，无法对其进行分析。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>50000043</p></td>
<td align="left"><p><em>WindowsInfo.xml</em> 缺少必需的元素。</p></td>
</tr>
<tr class="even">
<td align="left"><p>50000044</p></td>
<td align="left"><p>根据 XML 架构定义， <em>WindowsInfo.xml</em> 中的元素无效。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="wmis-query--0x7000xxxx-"></a>WMIS 查询 (0x7000xxxx)   
<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">错误代码</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>70000408</p></td>
<td align="left"><p>WMIS 服务器未关闭，但请求超时。</p></td>
</tr>
<tr class="even">
<td align="left"><p>70000500</p></td>
<td align="left"><p>WMIS 服务器返回了内部错误，但详细的错误代码不可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>70000503</p></td>
<td align="left"><p>WMIS 服务器正忙，无法处理请求。</p></td>
</tr>
</tbody>
</table>

 


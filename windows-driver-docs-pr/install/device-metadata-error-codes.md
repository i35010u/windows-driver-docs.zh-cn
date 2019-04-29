---
title: 设备元数据错误代码
description: 设备元数据错误代码
ms.assetid: 7ca3b9d3-8e7d-4421-affa-bddea2d4c262
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0724edeae8b219dd267367712229b3a9158f87e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357893"
---
# <a name="device-metadata-error-codes"></a>设备元数据错误代码


从 Windows 7 操作系统的以下错误代码为与下载相关的事件内的日志和处理的设备元数据包。 这些事件由事件跟踪 Windows (ETW) 服务，可通过使用事件查看器查看。 有关这些事件的详细信息，请参阅[调试设备元数据的包通过使用事件查看器](debugging-device-metadata-packages-by-using-event-viewer.md)。

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
<td align="left"><p>请求的批处理大小超出了最大值。</p></td>
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
<td align="left"><p>错误发生在服务端处理请求时。</p></td>
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
<td align="left"><p>没有任何本地元数据缓存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>40000012</p></td>
<td align="left"><p>本地元数据缓存中的结构 （文件夹） 不正确。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>40000021</p></td>
<td align="left"><p>不存在本地元数据存储。</p></td>
</tr>
<tr class="even">
<td align="left"><p>40000022</p></td>
<td align="left"><p>本地元数据存储区中的结构 （文件夹） 已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>40000031</p></td>
<td align="left"><p>找不到 dmrc 如何索引数据。</p></td>
</tr>
<tr class="even">
<td align="left"><p>40000032</p></td>
<td align="left"><p>Dmrc 如何索引数据已损坏。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="device-metadata-package-errors--0x500000xx-"></a>设备元数据包错误 (0x500000xx)  
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
<td align="left"><p><em>.Devicemetadata ms</em> cabinet (<em>cab</em>) 文件已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>50000012</p></td>
<td align="left"><p><em>.Devicemetadata ms</em> cab 文件不是正确的设备元数据结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>50000021</p></td>
<td align="left"><p><em>PackageInfo.xml</em>缺少。</p></td>
</tr>
<tr class="even">
<td align="left"><p>50000022</p></td>
<td align="left"><p><em>PackageInfo.xml</em>格式不正确，无法分析。</p>
<div class="alert">
<strong>请注意</strong>此错误代码包括用例其中任一<em>PackageInfo.xml</em>文档缺少必需的元素，或一个或多个它的元素不是有效的语法基于<a href="https://msdn.microsoft.com/library/windows/hardware/ff549614" data-raw-source="[PackageInfo XML Schema](https://msdn.microsoft.com/library/windows/hardware/ff549614)">PackageInfo XML架构</a>。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td align="left"><p>50000031</p></td>
<td align="left"><p><em>DeviceInfo.xml</em>缺少。</p></td>
</tr>
<tr class="even">
<td align="left"><p>50000032</p></td>
<td align="left"><p><em>DeviceInfo.xml</em>格式不正确，无法分析。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>50000033</p></td>
<td align="left"><p><em>DeviceInfo.xml</em>缺少所需的元素。</p></td>
</tr>
<tr class="even">
<td align="left"><p>50000034</p></td>
<td align="left"><p>中的元素<em>DeviceInfo.xml</em>不能基于 XML 架构定义。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>50000041</p></td>
<td align="left"><p><em>WindowsInfo.xml</em>缺少。</p></td>
</tr>
<tr class="even">
<td align="left"><p>50000042</p></td>
<td align="left"><p><em>WindowsInfo.xml</em>格式不正确，无法分析。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>50000043</p></td>
<td align="left"><p><em>WindowsInfo.xml</em>缺少所需的元素。</p></td>
</tr>
<tr class="even">
<td align="left"><p>50000044</p></td>
<td align="left"><p>中的元素<em>WindowsInfo.xml</em>不能基于 XML 架构定义。</p></td>
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
<td align="left"><p>WMIS 服务器不是向下，但该请求已超时。</p></td>
</tr>
<tr class="even">
<td align="left"><p>70000500</p></td>
<td align="left"><p>WMIS 服务器返回了内部错误，但详细的错误代码不可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>70000503</p></td>
<td align="left"><p>WMIS 服务器正忙，无法为请求提供服务。</p></td>
</tr>
</tbody>
</table>

 

 

 






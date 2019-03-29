---
title: 排查元数据创作向导的问题
description: 排查元数据创作向导的问题
ms.assetid: EBAF4289-DA23-4FFE-8CC0-DD21021CBA86
keywords:
- 故障排除创作向导的元数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0121ffa85d2c0886a7195a95dc930cd6f32f223
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464331"
---
# <a name="troubleshooting-the-metadata-authoring-wizards"></a>排查元数据创作向导的问题


\[本主题介绍提供在 Windows Driver Kit (WDK) 8 的设备元数据创作工具。 如果要开发 Windows 8.1 的设备体验，使用设备元数据创建向导附带[Microsoft Visual Studio 2013 和 Windows Driver Kit (WDK) 8.1](https://go.microsoft.com/fwlink/p/?LinkId=226411)。 有关详细信息，请参阅[Windows 8.1 设备体验](https://go.microsoft.com/fwlink/p/?linkid=325561)。 \]

如果收到以下错误消息中的任何操作，请参阅表中要解决此问题的解决方法列。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">工具</td>
<td align="left">屏幕</td>
<td align="left">错误消息</td>
<td align="left">分辨率</td>
</tr>
<tr class="even">
<td align="left">元数据创建向导</td>
<td align="left">欢迎</td>
<td align="left">错误：必须指定文件夹位置</td>
<td align="left">输入文件夹路径。</td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">欢迎</td>
<td align="left">错误：FolderLocation.Text 文件夹不存在</td>
<td align="left">更正的文件路径。</td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">欢迎</td>
<td align="left">所选的文件不存在</td>
<td align="left">更正文件路径或名称。</td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">欢迎</td>
<td align="left">XML 文件错误</td>
<td align="left"><p>更正 XML 错误。</p>
<p>错误示例：</p>
<ul>
<li>预期的第一个子级{0}要{1}，但找到{2}相反。</li>
<li>预期{0}后接{1}，但找到{2}相反。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">“完成”</td>
<td align="left">创建包失败：</td>
<td align="left"><p>更改的说明基础的参数。</p>
<p>错误示例：</p>
<ul>
<li>必须指定设备 ModelName (区域设置{0})</li>
<li>必须将此包与至少一个硬件 Id 或 ModelID 相关联</li>
<li>必须指定此设备的主类别</li>
</ul>
<p>警告示例：</p>
<ul>
<li>ModelNumber ({0}) 未指定</li>
<li>DeviceDescription 2 ({0}) 未指定</li>
<li>将由主类别选择确定通用图标</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">关联</td>
<td align="left">无效的格式："值"-不添加 {} 中的开头和结尾。</td>
<td align="left">删除{}，然后重试。</td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">关联</td>
<td align="left">无效的 GUID 格式："值"</td>
<td align="left">键入正确的 GUID，然后重试。</td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">图标</td>
<td align="left">有了图标文件出现问题："错误消息"图标验证错误</td>
<td align="left">图标找不到或不符合要求后，若要显示在设备和打印机控制面板中。 查找或修复图标，然后重试。
<p>错误示例：</p>
<ul>
<li>错误：需要设置图像 256 x 256 透明度。</li>
<li>错误：图像 48 x 48:32 位 + Alpha 不存在。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left">提交向导</td>
<td align="left">选择元数据包</td>
<td align="left">已存在具有该名称在列表中的包</td>
<td align="left">创建新的 GUID 的设备元数据包。</td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">选择元数据包</td>
<td align="left">加载包时出错：</td>
<td align="left">更改的说明基础的参数。</td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">“完成”</td>
<td align="left">创建提交包时出错：</td>
<td align="left">更改的说明基础的参数。</td>
</tr>
</tbody>
</table>

 

 

 






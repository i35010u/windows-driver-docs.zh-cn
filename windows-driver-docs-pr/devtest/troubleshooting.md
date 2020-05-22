---
title: 排查元数据创作向导的问题
description: 排查元数据创作向导的问题
ms.assetid: EBAF4289-DA23-4FFE-8CC0-DD21021CBA86
keywords:
- 元数据创作向导疑难解答
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c58d733fc51ca7e808ac5f558f0ffbacba9daa97
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769587"
---
# <a name="troubleshooting-the-metadata-authoring-wizards"></a>排查元数据创作向导的问题


\[本主题介绍 Windows 驱动程序工具包（WDK）8中提供的设备元数据创作工具。 如果正在开发 Windows 8.1 设备体验，请使用[Microsoft Visual Studio 2013 和 Windows 驱动程序工具包（WDK） 8.1](https://www.microsoft.com/download/details.aspx?id=42273)中提供的设备元数据创作向导。 \]

如果收到以下任何错误消息，请参阅表中的解决方法列以解决问题。

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
<td align="left">解决方法</td>
</tr>
<tr class="even">
<td align="left">元数据创作向导</td>
<td align="left">欢迎使用</td>
<td align="left">错误：必须指定文件夹位置</td>
<td align="left">输入文件夹路径。</td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">欢迎使用</td>
<td align="left">错误： FolderLocation 文件夹不存在</td>
<td align="left">更正文件路径。</td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">欢迎使用</td>
<td align="left">所选文件不存在</td>
<td align="left">更正文件路径或名称。</td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">欢迎使用</td>
<td align="left">XML 文件错误</td>
<td align="left"><p>更正 XML 错误。</p>
<p>错误示例：</p>
<ul>
<li>需要的第一个子级 {0} {1} ，但却找到了 {2} 。</li>
<li>的 {0} 后面应为 {1} ，但却找到了 {2} 。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">完成</td>
<td align="left">创建包失败：</td>
<td align="left"><p>根据说明更改参数。</p>
<p>错误示例：</p>
<ul>
<li>必须为设备指定 ModelName （区域设置 {0} ）</li>
<li>必须将此包与至少一个 HardwareID 或 ModelID 相关联</li>
<li>你必须指定此设备的主要类别</li>
</ul>
<p>警告示例：</p>
<ul>
<li>{0}未指定 ModelNumber （）</li>
<li>未指定 DeviceDescription 2 （ {0} ）</li>
<li>一般图标将由主类别选择决定</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">关联</td>
<td align="left">无效的格式： "Value"-不要在开头和结尾添加 {}。</td>
<td align="left">请删除 {} ，然后重试。</td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">关联</td>
<td align="left">无效的 GUID 格式： "Value"</td>
<td align="left">键入正确的 GUID，然后重试。</td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">图标</td>
<td align="left">图标文件出现问题： "错误消息" 图标验证错误</td>
<td align="left">找不到该图标，或者无法满足在 "控制面板" 的 "设备和打印机" 中显示的要求。 找到或修复图标，然后重试。
<p>错误示例：</p>
<ul>
<li>错误：需要设置图像256x256 透明度。</li>
<li>错误： Image 48x48：32位 + Alpha 不存在。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left">提交向导</td>
<td align="left">选择元数据包</td>
<td align="left">列表中已存在具有该名称的包</td>
<td align="left">为设备元数据包创建新的 GUID。</td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">选择元数据包</td>
<td align="left">加载包时出现问题：</td>
<td align="left">根据说明更改参数。</td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">完成</td>
<td align="left">创建提交包时出现问题：</td>
<td align="left">根据说明更改参数。</td>
</tr>
</tbody>
</table>

 

 

 






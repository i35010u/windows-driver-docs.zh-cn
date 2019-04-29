---
title: Bug 检查 0x9A SYSTEM_LICENSE_VIOLATION
description: SYSTEM_LICENSE_VIOLATION bug 检查具有 0x0000009A 值。 此 bug 检查指示已违反软件许可协议。
ms.assetid: 742d864c-46f8-4d7f-8617-061c75fe833a
keywords:
- Bug 检查 0x9A SYSTEM_LICENSE_VIOLATION
- SYSTEM_LICENSE_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SYSTEM_LICENSE_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 72b925fe2d92531a5f4886a9da3d4e3de466dd2e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324715"
---
# <a name="bug-check-0x9a-systemlicenseviolation"></a>Bug 检查 0x9A：系统\_许可证\_冲突


系统\_许可证\_冲突错误检查的值为 0x0000009A。 此 bug 检查指示已违反软件许可协议。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="systemlicenseviolation-parameters"></a>系统\_许可证\_冲突参数


参数 1 指示冲突的类型。 其他参数的含义取决于参数 1 的值。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00</p></td>
<td align="left"><p><strong>0:</strong>该产品应该是 WinNT</p>
<p><strong>1:</strong>该产品应该 LanmanNT 或 ServerNT</p></td>
<td align="left"><p>部分序列号</p></td>
<td align="left"><p>从产品选项键入该产品的前两个字符</p></td>
<td align="left"><p>已尝试脱机产品类型更改。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x01</p></td>
<td align="left"><p>从来源 1 的已注册的评估时间</p></td>
<td align="left"><p>部分序列号</p></td>
<td align="left"><p>备用源中的已注册的评估时间</p></td>
<td align="left"><p>已尝试对 Microsoft Windows 评估单位时间段的脱机更改。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x02</p></td>
<td align="left"><p>与打开失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法打开安装程序密钥。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x03</p></td>
<td align="left"><p>与键查找失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>SetupType 或 SetupInProgress 缺少的值从安装程序密钥，因此无法检测模式下安装程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x04</p></td>
<td align="left"><p>与键查找失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p><strong>SystemPrefix</strong>缺少从安装程序密钥的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x05</p></td>
<td align="left"><p>（请参阅安装程序代码）</p></td>
<td align="left"><p>许可处理器中找到无效的值</p></td>
<td align="left"><p>正式许可的处理器数</p></td>
<td align="left"><p>已尝试脱机更改为的许可处理器数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x06</p></td>
<td align="left"><p>与打开失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p><strong>产品</strong>无法打开密钥。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x07</p></td>
<td align="left"><p>与读取失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p><strong>ProductType</strong>无法读取值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x08</p></td>
<td align="left"><p>与更改通知失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>在更改通知<strong>产品</strong>失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x09</p></td>
<td align="left"><p>与更改通知失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>在更改通知<strong>SystemPrefix</strong>失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>NTW 系统已转换为 NTS 系统。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>与更改失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>安装程序密钥的引用失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>与更改失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>产品选项密钥的引用失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>与失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>尝试打开<strong>产品</strong>工作线程中失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>与失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>尝试打开安装程序密钥失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>与失败关联的状态代码</p></td>
<td align="left"><p><strong>0:</strong>设置失败的值</p>
<p><strong>1:</strong>更改通知失败</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>安装程序密钥的工作线程中出错。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"><p>与失败关联的状态代码</p></td>
<td align="left"><p><strong>0:</strong>设置失败的值</p>
<p><strong>1:</strong>更改通知失败</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>产品选项键辅助线程中出现错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x12</p></td>
<td align="left"><p>与失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法打开<strong>LicenseInfoSuites</strong>套件的密钥。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x13</p></td>
<td align="left"><p>与失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法查询<strong>LicenseInfoSuites</strong>套件的密钥。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x14</p></td>
<td align="left"><p>内存分配的大小</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法分配内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>与失败关联的状态代码</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法重置<strong>ConcurrentLimit</strong>套件的密钥的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>与失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法打开 suite 产品的许可证密钥。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x17</p></td>
<td align="left"><p>与失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法重置<strong>ConcurrentLimit</strong> suite 产品的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x18</p></td>
<td align="left"><p>与打开失败关联的状态代码</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法启动的更改通知<strong>LicenseInfoSuites</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x19</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>一套必须是 PDC 的系统上运行。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1A</p></td>
<td align="left"><p>与失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>枚举套件时出错。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1B</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>尝试对策略缓存的更改。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

Microsoft Windows 操作系统检测到软件许可协议的冲突。

用户可能已尝试进行更改脱机系统的产品类型或更改计算单元的 Windows 的试用期。 有关特定冲突的详细信息，请参阅参数列表。

 

 





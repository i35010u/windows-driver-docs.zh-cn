---
title: Bug 检查 0x9A SYSTEM_LICENSE_VIOLATION
description: SYSTEM_LICENSE_VIOLATION bug 检查的值为0x0000009A。 此 bug 检查指示违反了软件许可协议。
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
ms.openlocfilehash: dad067c73f979fc4b469511b88b00b63cd4fbdd5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839332"
---
# <a name="bug-check-0x9a-system_license_violation"></a>Bug 检查0x9A：系统 \_ 许可证 \_ 冲突


系统 \_ 许可证 \_ 冲突 bug 检查的值为0x0000009A。 此 bug 检查指示违反了软件许可协议。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="system_license_violation-parameters"></a>系统 \_ 许可证 \_ 冲突参数


参数1指示违规类型。 其他参数的意义取决于参数1的值。

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
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00</p></td>
<td align="left"><p><strong>0：</strong> 产品应为 WinNT</p>
<p><strong>1：</strong> 产品应是 LanmanNT 或 ServerNT</p></td>
<td align="left"><p>部分序列号</p></td>
<td align="left"><p>产品选项中的产品类型的前两个字符</p></td>
<td align="left"><p>已尝试进行脱机产品类型更改。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x01</p></td>
<td align="left"><p>源1中的已注册计算时间</p></td>
<td align="left"><p>部分序列号</p></td>
<td align="left"><p>来自备用源的已注册计算时间</p></td>
<td align="left"><p>已尝试脱机更改 Microsoft Windows 评估单元时间段。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x02</p></td>
<td align="left"><p>与打开失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法打开安装密钥。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x03</p></td>
<td align="left"><p>与键查找失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>缺少安装程序项中的 SetupType 或 SetupInProgress 值，因此无法检测到安装模式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x04</p></td>
<td align="left"><p>与键查找失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>缺少来自安装程序密钥的 <strong>SystemPrefix</strong> 值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x05</p></td>
<td align="left"><p> (查看安装代码) </p></td>
<td align="left"><p>在许可的处理器中发现无效值</p></td>
<td align="left"><p>正式许可的处理器数量</p></td>
<td align="left"><p>已尝试对已授权处理器的数量进行脱机更改。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x06</p></td>
<td align="left"><p>与打开失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法打开 <strong>ProductOptions</strong> 键。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x07</p></td>
<td align="left"><p>与读取失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法读取 <strong>ProductType</strong> 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x08</p></td>
<td align="left"><p>与更改通知失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>在 <strong>ProductOptions</strong> 上更改通知失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x09</p></td>
<td align="left"><p>与更改通知失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>在 <strong>SystemPrefix</strong> 上更改通知失败。</p></td>
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
<td align="left"><p>安装键的引用失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>与更改失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>产品选项键的引用失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>与失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>尝试在工作线程中打开 <strong>ProductOptions</strong> 失败。</p></td>
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
<td align="left"><p><strong>0：</strong> 设置值失败</p>
<p><strong>1：</strong> 更改通知失败</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>安装密钥工作线程中出现错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"><p>与失败关联的状态代码</p></td>
<td align="left"><p><strong>0：</strong> 设置值失败</p>
<p><strong>1：</strong> 更改通知失败</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>产品选项密钥工作线程中出现错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x12</p></td>
<td align="left"><p>与失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法打开套件的 <strong>LicenseInfoSuites</strong> 项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x13</p></td>
<td align="left"><p>与失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法查询套件的 <strong>LicenseInfoSuites</strong> 项。</p></td>
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
<td align="left"><p>预留</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法重置套件密钥的 <strong>ConcurrentLimit</strong> 值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>与失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法打开套件产品的许可证密钥。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x17</p></td>
<td align="left"><p>与失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法重置套件产品的 <strong>ConcurrentLimit</strong> 值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x18</p></td>
<td align="left"><p>与打开失败关联的状态代码</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法为 <strong>LicenseInfoSuites</strong>启动更改通知。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x19</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>套件在必须是 PDC 的系统上运行。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1A</p></td>
<td align="left"><p>与失败关联的状态代码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>枚举套件时出现错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1B</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已尝试更改策略缓存。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

Microsoft Windows 操作系统检测到违反软件许可协议。

用户可能尝试更改脱机系统的产品类型或更改 Windows 评估单元的试用期。 有关特定冲突的详细信息，请参阅参数列表。

 

 





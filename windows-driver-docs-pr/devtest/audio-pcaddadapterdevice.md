---
title: 'PcAddAdapterDevice 规则 (音频) '
description: PcAddAdapterDevice 规则指定 PortCls 微型端口驱动程序正确使用 PcAddAdapterDevice 函数，具体而言，DeviceExtensionSize 应为零 (0) 或小于端口 \_ 类的 \_ 设备 \_ 扩展 \_ 大小。
ms.assetid: AD020D31-9994-4AD1-A937-E29A594FC9D4
ms.date: 05/21/2018
keywords:
- 'PcAddAdapterDevice 规则 (音频) '
topic_type:
- apiref
api_name:
- PcAddAdapterDevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b50ecb9a9bf26823bd8346064c70e6924e706e29
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382819"
---
# <a name="pcaddadapterdevice-rule-audio"></a>PcAddAdapterDevice 规则 (音频) 


PcAddAdapterDevice 规则指定 PortCls 微型端口驱动程序正确使用 **PcAddAdapterDevice** 函数，具体而言， *DeviceExtensionSize* 应为零 (0) 或小于端口 \_ 类的 \_ 设备 \_ 扩展 \_ 大小。

**驱动程序模型：音频**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x00071007) 


<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>若要验证此规则，请打开 "命令提示符" 窗口。 输入 Driver Verifier 命令并指定 <strong>/domain 音频</strong>。</p>
<p>例如：</p>
<p><strong>verifier/domain 音频</strong>[<em>options</em>] <strong>/driver</strong> <em> &lt; yourdriver &gt; </em></p>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a>。</p></td>
</tr>
</tbody>
</table>

 

 


---
title: UPS ServiceProviders 注册表项
description: 创建每个 UPS 模型 UPS ServiceProviders 注册表项下的特定于供应商的子项。
ms.assetid: fa206f16-e136-4bfe-9823-7c324d62e1fb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfe58745ac5f9ae1f3e880932914d35b6d3481d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564905"
---
# <a name="upsserviceproviders-registry-entries"></a>UPS\\ServiceProviders 注册表项


## <span id="ddk_ups_serviceproviders_registry_entries_kg"></span><span id="DDK_UPS_SERVICEPROVIDERS_REGISTRY_ENTRIES_KG"></span>


下**UPS**\\**ServiceProviders**注册表项，UPS 供应商应创建一个特定于供应商的子项。 在此子项下供应商应创建为每个 UPS 模型的条目。 供应商必须创建这些注册表项时[安装 UPS 微型驱动程序](installing-ups-minidrivers.md)。

每个特定于模型的条目包含值名称和值。 值名称应为 UPS 模型的名称。 具有此名称关联的值是两个部分组成的字符串：

-   值字符串的第一部分表示识别模型的功能的十六进制位掩码。 下表中定义的位值。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">位值</th>
    <th align="left">描述</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>0x00000001</p></td>
    <td align="left"><p>安装 UPS。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>0x00000002</p></td>
    <td align="left"><p>UPS 支持电源故障通知。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>0x00000004</p></td>
    <td align="left"><p>UPS 支持电池电量不足的通知。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>0x00000008</p></td>
    <td align="left"><p>UPS 可以关闭使用串行端口。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>0x00000010</p></td>
    <td align="left"><p>电源故障通知表示正信号。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>0x00000020</p></td>
    <td align="left"><p>由正信号指示电池电量低通知。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>0x00000040</p></td>
    <td align="left"><p>情况正信号时，UPS 处于关闭状态。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>0x00000080</p></td>
    <td align="left"><p>保留。 不使用。</p></td>
    </tr>
    </tbody>
    </table>

     

-   字符串的第二部分是可选的。 它表示的路径和 UPS 微型驱动程序的名称。 如果提供此路径和名称，则它必须跟分号 （;）。 如果只提供名称，%systemroot%的默认路径\\使用 system32。

和 UPS 微型驱动程序安装后，系统管理员已启用，UPS 使用后**电源选项**，系统的 UPS 服务复制的型号特定**UPS** \\ **ServiceProviders**到其他，控制系统的注册表位置值。

以下是一家供应商的子项，使用的两个 UPS 模型，值名称和值的示例在**UPS**\\**ServiceProviders**:

``` syntax
UPS\ServiceProviders
    American Power Conversion
        Back-UPS "0x7f"
        Smart-UPS "0x1;apcups.dll"
```

 

 





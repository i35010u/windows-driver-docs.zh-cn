---
title: UPS ServiceProviders 注册表项
description: 在 UPS ServiceProviders 注册表项下为每个 UPS 模型创建供应商特定的子项。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ce4ae6b7d1021acca9f7ae904031f93327d92be
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784307"
---
# <a name="upsserviceproviders-registry-entries"></a>UPS \\ ServiceProviders 注册表项


## <span id="ddk_ups_serviceproviders_registry_entries_kg"></span><span id="DDK_UPS_SERVICEPROVIDERS_REGISTRY_ENTRIES_KG"></span>


在 **ups** \\ **ServiceProviders** 注册表项下，ups 供应商应创建特定于供应商的子项。 在此子项下，供应商应为每个 UPS 模型创建一个条目。 供应商必须在 [安装 UPS 微型驱动程序](installing-ups-minidrivers.md)时创建这些注册表项。

每个特定于模型的条目都包含一个值名称和一个值。 值名称应为 UPS 模型的名称。 与此名称关联的值是由两部分组成的字符串：

-   值字符串的第一部分表示用于标识模型功能的十六进制位掩码。 下表中定义了位值。

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
    <td align="left"><p>已安装 UPS。</p></td>
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
    <td align="left"><p>可以使用串行端口关闭 UPS。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>0x00000010</p></td>
    <td align="left"><p>电源故障通知用正信号表示。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>0x00000020</p></td>
    <td align="left"><p>电池电量不足通知用正信号表示。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>0x00000040</p></td>
    <td align="left"><p>使用正信号关闭 UPS。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>0x00000080</p></td>
    <td align="left"><p>保留。 请勿使用。</p></td>
    </tr>
    </tbody>
    </table>

     

-   字符串的第二部分是可选的。 它表示 UPS 微型驱动程序的路径和名称。 如果提供了此路径和名称，则该路径和名称前面必须有一个分号 (; ) 。 如果只提供名称，则使用% SystemRoot% system32 的默认路径 \\ 。

安装 ups 微型驱动程序之后，系统管理员使用 **电源选项** 启用了 ups 后，系统的 ups 服务会将特定于模型的 **ups** \\ **ServiceProviders** 值复制到系统控制的其他注册表位置。

下面是一个供应商子项的示例，其中包含两个 ups 模型的值名称和值，位于 **ups** \\ **ServiceProviders** 下：

``` syntax
UPS\ServiceProviders
    American Power Conversion
        Back-UPS "0x7f"
        Smart-UPS "0x1;apcups.dll"
```

 

 





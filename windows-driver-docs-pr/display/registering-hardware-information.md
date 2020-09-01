---
title: 注册硬件信息
description: 注册硬件信息
ms.assetid: 1fec9fcf-3ec7-4926-9ceb-ef1f7f42e963
keywords:
- 注册表 WDK 显示
- 注册表 WDK 显示中的硬件信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29bbf383ccc71796b4f083881424bab314371645
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067270"
---
# <a name="registering-hardware-information"></a>注册硬件信息


若要向用户显示有用的信息并帮助调试，显示微型端口驱动程序必须在注册表中设置某些硬件信息。 显示微型端口驱动程序必须设置芯片类型、数字到模拟转换器 (DAC) 类型、内存大小 () 适配器以及用于标识适配器的字符串。 此信息显示在 "控制面板" 的 " **显示** 应用程序" 中。 通常，驱动程序将此信息设置为其 [**DxgkDdiAddDevice**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_add_device) 函数。

若要设置此信息，驱动程序：

1.  调用 **IoOpenDeviceRegistryKey** 来存储特定于驱动程序的信息。 在此调用中，驱动程序在 \_ \_ *DevInstKeyType*参数中指定 PLUGPLAY REGKEY 驱动程序标志，并 \_ 在 \_ DesiredAccess 参数中指定密钥集值、键 \_ 写入或键 \_ 所有 \_ 访问值。 *DesiredAccess*

2.  多次调用 [**ZwSetValueKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwsetvaluekey) 函数，以设置每种类型的硬件信息。 在每次调用中，驱动程序在 *KeyHandle* 参数中指定从 **IoOpenDeviceRegistryKey**获取的软件密钥句柄。

    下表描述了驱动程序必须注册的信息，并提供了**ZwSetValueKey**的*ValueName*和*Data*参数的详细信息：

    <table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">输入信息</th>
    <th align="left"><em>ValueName</em> 参数</th>
    <th align="left"><em>Data</em> 参数</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>芯片类型</p></td>
    <td align="left"><p>HardwareInformation.ChipType</p></td>
    <td align="left"><p>包含芯片名称的以 Null 结尾的字符串</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>DAC 类型</p></td>
    <td align="left"><p>HardwareInformation. DacType</p></td>
    <td align="left"><p>以 Null 结尾的字符串，其中包含 DAC 名称或标识符 (ID) </p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>内存大小</p></td>
    <td align="left"><p>HardwareInformation. MemorySize</p></td>
    <td align="left"><p>ULONG，其中包含适配器上的视频内存量（以 mb 为单位）</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>适配器 ID</p></td>
    <td align="left"><p>HardwareInformation.AdapterString</p></td>
    <td align="left"><p>包含适配器名称的以 Null 结尾的字符串</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>BIOS</p></td>
    <td align="left"><p>HardwareInformation.BiosString</p></td>
    <td align="left"><p>以 Null 结尾的字符串，其中包含有关 BIOS 的信息</p></td>
    </tr>
    </tbody>
    </table>

     

 


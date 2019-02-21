---
title: 注册硬件信息
description: 注册硬件信息
ms.assetid: 1fec9fcf-3ec7-4926-9ceb-ef1f7f42e963
keywords:
- 注册表 WDK 显示
- 在注册表 WDK 显示的硬件信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca8910e3aafbbc0532a6694a9f7db9ea3405cd00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521980"
---
# <a name="registering-hardware-information"></a>注册硬件信息


若要显示有用的信息，向用户和有关中调试的帮助，请显示微型端口驱动程序必须在注册表中设置特定硬件的信息。 显示微型端口驱动程序必须设置芯片类型、 数字模拟转换器 (DAC) 类型、 内存大小 （的适配器） 和一个字符串来标识该适配器。 情况下显示此信息**显示**控制面板中的应用程序。 通常情况下，驱动程序设置此信息其[ **DxgkDdiAddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff559586)函数。

若要设置此信息，该驱动程序：

1.  调用**IoOpenDeviceRegistryKey**用于存储特定于驱动程序的信息。 在此调用中，该驱动程序指定 PLUGPLAY\_REGKEY\_中的驱动程序标志*DevInstKeyType*参数和该键\_设置\_值、 密钥\_写入或密钥\_所有\_中的访问值*DesiredAccess*参数。

2.  调用[ **ZwSetValueKey** ](https://msdn.microsoft.com/library/windows/hardware/ff567109)函数多次以设置每种类型的硬件信息。 在每个调用中，该驱动程序指定，在*KeyHandle*参数，请从已获取的软件密钥句柄**IoOpenDeviceRegistryKey**。

    下表描述的信息，该驱动程序必须注册，并提供详细信息*ValueName*并*数据*的参数**ZwSetValueKey**:

    <table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">条目的信息</th>
    <th align="left"><em>ValueName</em>参数</th>
    <th align="left"><em>数据</em>参数</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>芯片类型</p></td>
    <td align="left"><p>HardwareInformation.ChipType</p></td>
    <td align="left"><p>包含的芯片名称的以 null 结尾的字符串</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>DAC 类型</p></td>
    <td align="left"><p>HardwareInformation.DacType</p></td>
    <td align="left"><p>以 null 结尾的字符串，包含 DAC 名称或标识符 (ID)</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>内存大小</p></td>
    <td align="left"><p>HardwareInformation.MemorySize</p></td>
    <td align="left"><p>以兆字节表示，包含在适配器上的视频内存量的 ULONG</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>适配器 ID</p></td>
    <td align="left"><p>HardwareInformation.AdapterString</p></td>
    <td align="left"><p>包含适配器的名称的以 null 结尾的字符串</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>BIOS</p></td>
    <td align="left"><p>HardwareInformation.BiosString</p></td>
    <td align="left"><p>以 null 结尾的字符串，其中包含有关 BIOS 的信息</p></td>
    </tr>
    </tbody>
    </table>

     

 

 






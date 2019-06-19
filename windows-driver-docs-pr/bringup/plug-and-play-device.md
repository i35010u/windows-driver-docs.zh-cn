---
title: 即插即用设备
description: ESRT 配置表存在将直接 Windows 来枚举每个固件资源的单独的即插即用设备实例。
ms.assetid: 85EE32E7-1871-490D-9FF6-07E0891C78E3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: beb3b3ebb01f4e364af2ec95be235fa9ce294de6
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161361"
---
# <a name="plug-and-play-device"></a>即插即用设备


ESRT 配置表存在将直接 Windows 来枚举每个固件资源的单独的即插即用设备实例。 对于匹配目的的驱动程序，由其硬件 Id，将嵌入固件 ID GUID 唯一标识固件资源设备。 引用中的 ESRT 示例[ESRT 表定义](esrt-table-definition.md)，枚举了相应的设备实例。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>设备实例 ID</th>
<th>硬件 ID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UEFI\RES_{SYSTEM_FIRMWARE}\0</td>
<td><p>UEFI\RES_{SYSTEM_FIRMWARE}&REV_1</p>
<p>UEFI\RES_{SYSTEM_FIRMWARE}</p></td>
</tr>
<tr class="even">
<td>UEFI\RES_{DEVICE_FIRMWARE}\0</td>
<td><p>UEFI\RES_{DEVICE_FIRMWARE}&REV_1</p>
<p>UEFI\RES_{DEVICE_FIRMWARE}</p></td>
</tr>
</tbody>
</table>

 

请注意，这两个硬件 Id 设备报告的每个固件资源;第一个硬件 ID 包括最新的固件资源版本，而第二个却没有。 由于固件资源版本应作为应用固件更新的结果而改变，因此非常重要的第二个取消版本控制的硬件 ID 针对驱动程序，以便它可以是适用于安装在所有固件资源版本，无论哪一个版本是当前提供给定系统上。

## <a name="related-topics"></a>相关主题
[ESRT 表定义](esrt-table-definition.md)  
[创作更新驱动程序包](authoring-an-update-driver-package.md)  
[处理更新](processing-updates.md)  
[设备 I/O 从 UEFI 环境](device-i-o-from-the-uefi-environment.md)  
[无缝危机预防和恢复](seamless-crisis-prevention-and-recovery.md)  
[固件更新状态](firmware-update-status.md)  




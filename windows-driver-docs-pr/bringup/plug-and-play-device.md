---
title: 即插即用设备
description: 如果存在 ESRT 配置表，则会将 Windows 定向到每个固件资源的单独 PnP 设备实例。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8419649af9b9366deb2f32d553bfd0b209b43cf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783597"
---
# <a name="plug-and-play-device"></a>即插即用设备


如果存在 ESRT 配置表，则会将 Windows 定向到每个固件资源的单独 PnP 设备实例。 出于驱动程序匹配的目的，固件资源设备由其硬件 Id 唯一标识，这些 Id 嵌入了固件 ID GUID。 引用 [ESRT 表定义](esrt-table-definition.md)中的 ESRT 示例时，会枚举相应的设备实例。

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
<td>UEFI \ RES_ {SYSTEM_FIRMWARE} \ 0</td>
<td><p>UEFI \ RES_ {SYSTEM_FIRMWARE} &REV_1</p>
<p>UEFI \ RES_ {SYSTEM_FIRMWARE}</p></td>
</tr>
<tr class="even">
<td>UEFI \ RES_ {DEVICE_FIRMWARE} \ 0</td>
<td><p>UEFI \ RES_ {DEVICE_FIRMWARE} &REV_1</p>
<p>UEFI \ RES_ {DEVICE_FIRMWARE}</p></td>
</tr>
</tbody>
</table>

 

请注意，每个固件资源设备报告了两个硬件 Id;第一个硬件 ID 包含当前固件资源版本，而第二个硬件 ID 则不包含。 由于应用固件更新的原因，固件资源版本应会更改，因此，驱动程序必须针对第二个不受版本控制的硬件 ID，以便它适用于所有固件资源版本中的安装，而与给定系统当前存在的版本无关。

## <a name="related-topics"></a>相关主题
[ESRT 表定义](esrt-table-definition.md)  
[创作更新驱动程序包](authoring-an-update-driver-package.md)  
[处理更新](processing-updates.md)  
[来自 UEFI 环境的设备 I/O](device-i-o-from-the-uefi-environment.md)  
[无缝危机预防和恢复](seamless-crisis-prevention-and-recovery.md)  
[固件更新状态](firmware-update-status.md)  




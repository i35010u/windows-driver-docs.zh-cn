---
title: IPM 硬盘驱动器空闲超时
description: IPM 硬盘驱动器空闲超时
ms.assetid: 1dcc261a-803c-4c0e-a68e-29b00f46cd32
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4dd731f1b57f8c4c6050431247ae0302f6286bf2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378737"
---
# <a name="ipm-hard-disk-drive-idle-timeout"></a>IPM 硬盘驱动器空闲超时


虽然硬盘驱动器 (HDD) 不是典型的移动 PC 中的主电源使用者，可以通过下 HDD 介质旋转实现节能。 HDD 空闲超时允许 Windows 停止 HDD 媒体会自动旋转后一小段磁盘读取和写入处于非活动状态。

因品牌和型号的 HDD 而异时 HDD 媒体片降速时实现节能。 我们鼓励系统制造商可以使用 HDD 供应商以确定特定设备的最佳 HDD 空闲超时值。

默认情况下，Windows Vista 指定较长的 HDD 空闲超时值。 系统制造商应考虑时想要实现主动电池节省移动 Pc 上的指定更短的值。 下表总结了 HDD 空闲设置的详细信息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>详细信息</strong></p></td>
<td align="left"><p><strong>说明</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>友好名称</p></td>
<td align="left"><p>关闭后的硬盘</p></td>
</tr>
<tr class="odd">
<td align="left"><p>描述</p></td>
<td align="left"><p>指定磁盘关闭前的硬盘驱动器多长时间处于非活动状态</p></td>
</tr>
<tr class="even">
<td align="left"><p>PowerCfg 别名</p></td>
<td align="left"><p>DISKIDLE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>组策略路径</p></td>
<td align="left"><p>从硬盘管理 \ Management\Hard 磁盘 Settings\Turn</p></td>
</tr>
<tr class="even">
<td align="left"><p>GUID</p></td>
<td align="left"><p>6738e2c4-e8a5-4a42-b16a-e040e769756e</p></td>
</tr>
<tr class="odd">
<td align="left"><p>在中定义</p></td>
<td align="left"><p>Ntpoapi.h</p></td>
</tr>
<tr class="even">
<td align="left"><p>平衡的默认值</p></td>
<td align="left"><p>60 分钟 (AC) 30 分钟 (DC)</p></td>
</tr>
</tbody>
</table>

 

有关详细信息请参阅[移动电池寿命解决方案适用于移动平台专业人员的指南。](https://go.microsoft.com/fwlink/p/?linkid=144534)

 

 





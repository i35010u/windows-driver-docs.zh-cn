---
title: ESRT 表定义
description: 指向 ESRT 表的标识通过 EFI_CONFIGURATION_TABLE 中其相应的 GUID。
ms.assetid: F332CCF3-AE6D-4B02-A63E-DB05910C8E6E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17b7f46d926c20be7b920c31848401b782d3c24c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337592"
---
# <a name="esrt-table-definition"></a>ESRT 表定义


通过在 EFI 中其相应的 GUID 标识 ESRT 表指向\_配置\_表。

```cpp
#define EFI_SYSTEM_RESOURCE_TABLE_GUID   \
{ 0xb122a263, 0x3661, 0x4f68,  0x99, 0x29, 0x78, 0xf8, 0xb0, 0xd6, 0x21, 0x80  }
```

下表介绍 ESRT 表和表中包含的固件资源条目的格式。

<table>
<colgroup>
<col width="20%" />
<col width="10%" />
<col width="10%" />
<col width="10%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>字段</th>
<th>数组值</th>
<th>字节长度</th>
<th>字节偏移量</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>固件资源计数</td>
<td></td>
<td>4</td>
<td>0</td>
<td>在 ESRT 固件资源条目数。 不能为零。</td>
</tr>
<tr class="even">
<td>固件资源最大值</td>
<td></td>
<td>4</td>
<td>4</td>
<td>可以添加，而重新分配表的资源数组项的数目上限。 必须是大于或等于对固件资源计数。</td>
</tr>
<tr class="odd">
<td>资源的固件版本</td>
<td></td>
<td>8</td>
<td>8</td>
<td>固件资源条目版本。 此值应设置为 1。</td>
</tr>
<tr class="even">
<td>固件资源条目数组</td>
<td></td>
<td></td>
<td></td>
<td>固件资源条目 0</td>
</tr>
<tr class="odd">
<td></td>
<td>固件类</td>
<td>16</td>
<td>16</td>
<td>标识可通过更新 capsule 更新固件组件的 GUID。 此 GUID 将传递到 UEFI 更新封装运行时服务作为更新封装标头的 CapsuleGuid 参数更新过程。</td>
</tr>
<tr class="even">
<td></td>
<td>固件类型</td>
<td>4</td>
<td>32</td>
<td>标识的固件资源类型的以下值之一：
<ul>
<li>0:Unknown</li>
<li>1：系统固件</li>
<li>2：设备固件</li>
<li>3：UEFI 驱动程序</li>
</ul></td>
</tr>
<tr class="odd">
<td></td>
<td>固件版本</td>
<td>4</td>
<td>36</td>
<td>最新固件版本，其中一个更大的数字，表示较新版本。 此值的格式未定义，但应将主版本号和次版本号。 建议的格式为 first 主要 word，第二个字是次要版本号。</td>
</tr>
<tr class="even">
<td></td>
<td>最低受支持的固件版本</td>
<td>4</td>
<td>40</td>
<td>向其固件资源可以回滚对于给定的系统/设备最低固件资源版本。 如果在此固件版本中可用的安全相关的修补程序，至少兼容的版本应等于当前的固件版本。</td>
</tr>
<tr class="odd">
<td></td>
<td>封装标志</td>
<td>4</td>
<td>44</td>
<td>将传递到 UEFI 的标志位 0 – 15 （OS 是负责配置部分 7.5.3 UEFI 规范的定义的标志的位 16 日至 31 日） 的更新封装标头的 Flags 字段中的封装运行时服务更新。</td>
</tr>
<tr class="even">
<td></td>
<td>上次尝试版本</td>
<td>4</td>
<td>48</td>
<td>为其尝试更新最后一个固件版本。 此值作为固件版本使用相同的格式。</td>
</tr>
<tr class="odd">
<td></td>
<td>上次尝试的状态</td>
<td>4</td>
<td>52</td>
<td>尝试介绍的最后一个固件更新状态的以下值之一：
<ul>
<li>0:成功</li>
<li>1：不成功</li>
<li>2：资源不足</li>
<li>3：版本不正确</li>
<li>4:无效的图像格式</li>
<li>5:身份验证错误</li>
<li>6:电源事件的未连接的交流</li>
<li>7:电源事件-不足电池</li>
</ul></td>
</tr>
<tr class="even">
<td> ...</td>
<td></td>
<td></td>
<td></td>
<td>固件资源条目 1</td>
</tr>
</tbody>
</table>

 

核心 UEFI 固件应分配和填充 ESRT 配置表为自身 （系统固件） 中包含一个系统资源条目。 出于说明目的，在此指南 core 固件还将创建一个表示支持使用固件更新包机制进行设备固件更新的设备的其他条目。

必须始终有恰好一个描述系统固件的条目。 使用此项以目标系统固件更新。 如果实现执行系统和设备固件更新作为一个整体的操作，系统固件条目必须用于目标更新。 在所有其他情况下，设备固件更新针对 ESRT 条目描述设备固件的。

第一步则是生成 Guid 以表示这两个固件资源，即 {SYSTEM\_固件} 和 {设备\_固件}。 表 2 显示了表定义的示例。 此示例假定这两个固件版本当前是第 1 版 (固件版本 = = 1)。

| 字段                         | 数组值                       | ReplTest1                     | 备注                                                                                                            |
|-------------------------------|-----------------------------------|---------------------------|--------------------------------------------------------------------------------------------------------------------|
| 固件资源计数       |                                   | 2                         | 此表包含两个固件资源条目。                                                                 |
| 固件资源最大值     |                                   | 2                         | 此表分配包含足够的空间来描述最多为两个资源。                                |
| 资源的固件版本     |                                   | 1                         | 此表使用的固件资源条目格式版本为 1。                                                   |
| 固件资源条目数组 |                                   | 固件资源条目 0 |                                                                                                                    |
|                               | 固件类                    | (系统\_固件)        | 此 GUID 标识通过即插即用更新的系统固件。                                                       |
|                               | 固件类型                     | 1                         | 系统固件类型为 1。                                                                                         |
|                               | 固件版本                  | 1                         | 当前的系统固件版本为 1。                                                                          |
|                               | 最低受支持的固件版本 | 1                         | 最低受支持的固件版本为 1，因此固件不能将其回滚到版本早于版本 1。 |
|                               | 封装标志                     | 0                         | 系统固件没有定义任何专用的封装更新标志。                                                   |
|                               | 上次尝试版本              | 1                         | 为其尝试更新最后一个系统固件版本是版本 1。                                  |
|                               | 上次尝试的状态               | 0                         | 最后一个系统固件更新尝试成功。                                                            |
|                               |                                   | 固件资源条目 1 |                                                                                                                    |
|                               | 固件类                    | (设备\_固件)        | 此 GUID 标识通过即插即用更新设备固件。                                                       |
|                               | 固件类型                     | 2                         | 设备固件类型为 2。                                                                                         |
|                               | 固件版本                  | 1                         | 当前设备固件版本为 1。                                                                          |
|                               | 最低受支持的固件版本 | 1                         | 最低受支持的固件版本为 1，因此固件无法回滚到版本早于版本 1。 |
|                               | 封装标志                     | 0x8010                    | 设备固件定义专用封装更新标志 (0x8010)。                                                     |
|                               | 上次尝试版本              | 1                         | 为其尝试更新最后一个设备固件版本是版本 1                                    |
|                               | 上次尝试的状态               | 0                         | 最后一次设备固件更新尝试成功。                                                            |

 

上面的 ESRT 示例中用于其他位置在本文档中演示固件更新过程并描述对更新过程，以及支持的固件实现的 Windows 支持。

## <a name="related-topics"></a>相关主题
[Plug and play 设备](plug-and-play-device.md)  
[创作更新驱动程序包](authoring-an-update-driver-package.md)  
[处理更新](processing-updates.md)  
[设备 I/O 从 UEFI 环境](device-i-o-from-the-uefi-environment.md)  
[无缝危机预防和恢复](seamless-crisis-prevention-and-recovery.md)  
[固件更新状态](firmware-update-status.md)  




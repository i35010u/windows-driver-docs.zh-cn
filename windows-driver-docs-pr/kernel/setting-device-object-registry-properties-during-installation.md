---
title: 在安装期间设置设备对象注册表属性
description: 在安装期间设置设备对象注册表属性
keywords:
- 设备对象 WDK 内核，注册表
- 注册表 WDK 设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4243fee8c07f01209b87cdf18cb965dd227a185
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837983"
---
# <a name="setting-device-object-registry-properties-during-installation"></a>在安装期间设置设备对象注册表属性





若要在安装过程中设置设备对象属性，您必须提供指定属性的 INF 文件。 你可以为设备或设备安装程序类指定设备对象属性。

它们按如下方式指定。

-   对于单个设备，可在设备的 " *添加-注册表" 部分* 中设置属性。 设备的 *DDInstall* 中的 INF **AddReg** 指令。HW 部分指定设备的 "*添加注册表" 部分*。

-   对于设备安装程序类，在设备安装程序类的 " *添加-注册表" 部分* 设置属性。 类的 **ClassInstall32** 部分中的 INF **AddReg** 指令指定类的 "*添加注册表" 部分*。

在 " *添加注册表" 部分* 中，可以使用以下关键字指定要设置的单个设备对象属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>关键字</th>
<th>设备对象属性</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DeviceType</strong></p></td>
<td><p>设备类型</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceCharacteristics</strong></p></td>
<td><p>设备特征</p></td>
</tr>
<tr class="odd">
<td><p><strong>独占</strong></p></td>
<td><p>排他</p></td>
</tr>
<tr class="even">
<td><p><strong>安全性</strong></p></td>
<td><p>安全描述符</p></td>
</tr>
</tbody>
</table>

 

有关使用这些关键字的详细信息，请参阅 [**INF AddReg 指令**](../install/inf-addreg-directive.md)。

可以通过使用设备安装功能来设置用户模式组件的设置。 有关详细信息，请参阅 [安装后设置设备对象注册表属性](setting-device-object-registry-properties-after-installation.md)。

 


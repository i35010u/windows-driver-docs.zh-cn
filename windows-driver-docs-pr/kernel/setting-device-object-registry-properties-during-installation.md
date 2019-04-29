---
title: 在安装期间设置设备对象注册表属性
description: 在安装期间设置设备对象注册表属性
ms.assetid: 29d40398-09b9-4e64-aa47-da229066bffd
keywords:
- 设备对象 WDK 内核注册表
- 注册表 WDK 设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf560b528f01f4c22d04d8933a7e9342446da804
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385531"
---
# <a name="setting-device-object-registry-properties-during-installation"></a>在安装期间设置设备对象注册表属性





若要在安装过程中设置设备对象属性，必须提供指定的属性的 INF 文件。 可以指定设备的设备或设备安装程序类的对象属性。

按如下所示指定这些。

-   对于对单个设备设置的属性*添加注册表部分*设备。 INF **AddReg**指令中的设备*DDInstall*。硬件部分指定*添加注册表部分*设备。

-   设备安装程序类，属性中设置*添加注册表部分*设备安装程序类。 INF **AddReg**指令内**ClassInstall32**部分为类指定*添加注册表部分*类。

内*添加注册表部分*，可以使用下列关键字来指定要设置的单个设备对象属性。

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
<td><p><strong>Exclusive</strong></p></td>
<td><p>独占</p></td>
</tr>
<tr class="even">
<td><p><strong>安全性</strong></p></td>
<td><p>安全描述符</p></td>
</tr>
</tbody>
</table>

 

有关使用这些关键字的详细信息，请参阅[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)。

可以将的设置的用户模式组件，使用的设备安装功能。 有关详细信息，请参阅[设置设备对象注册表属性之后安装](setting-device-object-registry-properties-after-installation.md)。

 

 





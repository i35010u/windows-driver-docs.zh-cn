---
title: 打开注册表项对象的句柄
description: 打开注册表项对象的句柄
ms.assetid: 451e36a1-1cc2-469e-9f54-c02fef7b1666
keywords:
- 注册表 WDK 内核，对象例程
- 驱动程序注册表信息 WDK 内核，对象例程
- 对象例程 WDK 内核
- 注册表项对象 WDK 内核
- 打开注册表项对象句柄
- 注册表项对象 WDK 内核的句柄
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41051871ed71f806dd6d8f6c8727a19759b97871
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352064"
---
# <a name="opening-a-handle-to-a-registry-key-object"></a>打开注册表项对象的句柄





若要打开注册表项对象的句柄，请执行以下两步过程：

1.  创建[**对象\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff557749)结构，并将其初始化通过调用[ **InitializeObjectAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff547804)。 指定要作为操作的密钥名称*ObjectName*参数**InitializeObjectAttributes**。

    如果传递**NULL**作为*RootDirectory*参数**InitializeObjectAttributes**， *ObjectName*必须是完整路径注册表项，开头 **\\注册表**。 否则为*RootDirectory*必须是开放句柄注册表项，并*ObjectName*是相对于该注册表项的路径。

2.  通过调用打开的键对象的句柄[ **ZwCreateKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566425)或[ **ZwOpenKey**](https://msdn.microsoft.com/library/windows/hardware/ff567014)，并将传递**对象\_属性**到它的结构。 如果尚不存在密钥， **ZwCreateKey**将创建密钥，而**ZwOpenKey**将返回状态\_对象\_名称\_不\_找到。

您传递*DesiredAccess*参数**ZwCreateKey**或**ZwOpenKey** ，其中包含你请求的访问权限。 必须指定将执行允许您的驱动程序的操作的访问权限。 下表列出了可以执行的操作和相应的访问权限，以请求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>操作</th>
<th>所需的访问权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>获取注册表项值。</p></td>
<td><p>KEY_QUERY_VALUE 或 KEY_READ</p></td>
</tr>
<tr class="even">
<td><p>将注册表项值设置。</p></td>
<td><p>KEY_SET_VALUE 或 KEY_WRITE</p></td>
</tr>
<tr class="odd">
<td><p>遍历所有项的子项。</p></td>
<td><p>KEY_ENUMERATE_SUB_KEYS 或 KEY_READ</p></td>
</tr>
<tr class="even">
<td><p>创建一个子项。</p></td>
<td><p>KEY_CREATE_SUB_KEY 或 KEY_WRITE</p></td>
</tr>
<tr class="odd">
<td><p>删除密钥。</p></td>
<td><p>DELETE</p></td>
</tr>
</tbody>
</table>

 

有关可用值的详细信息*DesiredAccess*参数，请参阅[ **ZwCreateKey**](https://msdn.microsoft.com/library/windows/hardware/ff566425)。

您还可以调用[ **IoOpenDeviceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549443)并[ **IoOpenDeviceInterfaceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549433)打开到这些注册表项句柄分别，为特定于设备和特定于设备接口。 有关详细信息，请参阅[即插即用和播放注册表例程](plug-and-play-registry-routines.md)。

**请注意**  对的调用**ZwCreateKey**， **ZwOpenKey**， **IoOpenDeviceRegistryKey**，和**IoOpenDeviceInterfaceRegistryKey**，通用访问权限，泛型\_读取和泛型\_编写，在特定于密钥的访问权限，密钥的含义是等效的\_读取和密钥\_编写，分别，并可以在彼此替代这些特定于密钥的访问权限。

 

 

 





---
title: 打开注册表项对象的句柄
description: 打开注册表项对象的句柄
ms.assetid: 451e36a1-1cc2-469e-9f54-c02fef7b1666
keywords:
- 注册表 WDK 内核，对象例程
- 驱动程序注册表信息 WDK 内核，对象例程
- 对象例程 WDK 内核
- 注册表-密钥对象 WDK 内核
- 打开注册表项句柄-密钥对象
- 注册表-密钥对象 WDK 内核的句柄
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3930834ecf7265cc333f516c9b98a4c0ccda4852
ms.sourcegitcommit: a5f76805387760730faed5674d87201ec85b7dd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90112098"
---
# <a name="opening-a-handle-to-a-registry-key-object"></a>打开注册表项对象的句柄





若要打开注册表项对象的句柄，请执行以下两步过程：

1.  创建 [**对象 \_ 属性**](/windows/win32/api/ntdef/ns-ntdef-_object_attributes) 结构，并通过调用 [**InitializeObjectAttributes**](/windows/win32/api/ntdef/nf-ntdef-initializeobjectattributes)对其进行初始化。 指定要作为 *ObjectName* 参数 **InitializeObjectAttributes**的密钥的名称。

    如果将**NULL**作为*RootDirectory*参数传递给**InitializeObjectAttributes**，则*ObjectName*必须是注册表项的完整路径（从** \\ 注册表**开始）。 否则， *RootDirectory* 必须是密钥的开放句柄，并且 *ObjectName* 是相对于该密钥的路径。

2.  通过调用 [**ZwCreateKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey) 或 [**ZwOpenKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey)打开密钥对象的句柄，并向其传递 **对象 \_ 特性** 结构。 如果该项尚不存在， **ZwCreateKey** 将创建该密钥，而 **ZwOpenKey** 将返回 " \_ \_ \_ 找不到状态对象名称" \_ 。

将 *DesiredAccess* 参数传递给 **ZwCreateKey** 或 **ZwOpenKey** ，其中包含请求的访问权限。 您必须指定允许您的驱动程序执行的操作的访问权限。 下表列出了你可以执行的操作以及要请求的相应访问权限。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>操作</th>
<th>必需的访问权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>获取注册表项值。</p></td>
<td><p>KEY_QUERY_VALUE 或 KEY_READ</p></td>
</tr>
<tr class="even">
<td><p>设置注册表项值。</p></td>
<td><p>KEY_SET_VALUE 或 KEY_WRITE</p></td>
</tr>
<tr class="odd">
<td><p>循环遍历某个键的所有子项。</p></td>
<td><p>KEY_ENUMERATE_SUB_KEYS 或 KEY_READ</p></td>
</tr>
<tr class="even">
<td><p>创建子项。</p></td>
<td><p>KEY_CREATE_SUB_KEY 或 KEY_WRITE</p></td>
</tr>
<tr class="odd">
<td><p>删除密钥。</p></td>
<td><p>DELETE</p></td>
</tr>
</tbody>
</table>

 

有关 *DesiredAccess* 参数的可用值的详细信息，请参阅 [**ZwCreateKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey)。

你还可以调用 [**IoOpenDeviceRegistryKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey) 和 [**IoOpenDeviceInterfaceRegistryKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey) ，以打开特定于设备特定和设备接口的注册表项的句柄。 有关详细信息，请参阅 [即插即用注册表例程](plug-and-play-registry-routines.md)。

**注意**   对于对**ZwCreateKey**、 **ZwOpenKey**、 **IoOpenDeviceRegistryKey**和**IoOpenDeviceInterfaceRegistryKey**的调用，一般访问权限、泛型 \_ 读写和泛型 \_ 写入等效于密钥特定的访问权限、密钥 \_ 读取和密钥 \_ 写入，并可用作这些特定于密钥的访问权限。

 

 


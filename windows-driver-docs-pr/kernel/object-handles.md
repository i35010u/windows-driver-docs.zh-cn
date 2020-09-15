---
title: 对象句柄
description: 对象句柄
ms.assetid: deeeb3c0-54e4-4727-ac43-6da79be515d7
keywords:
- 对象处理 WDK 用户模式
- 对象处理 WDK 内核
- 处理 WDK 用户模式
- 处理 WDK 内核
- 私有对象处理 WDK
- 共享对象处理 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d8f77f4e4c353dadfa0734db84f3205f3d09a3a
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106338"
---
# <a name="object-handles"></a>对象句柄





驱动程序和用户模式组件通过 *句柄*访问大多数系统定义的对象。 句柄由 "句柄不透明" 数据类型表示。  (请注意，句柄不用于访问设备对象或驱动程序对象。 ) 

对于大多数对象类型，创建或打开对象的内核模式例程提供调用方的句柄。 然后，调用方在对象的后续操作中使用该句柄。

下面是驱动程序通常使用的对象类型的列表，以及提供该类型的对象的句柄的例程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>对象类型</th>
<th>对应的创建/打开例程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>文件</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile" data-raw-source="[&lt;strong&gt;IoCreateFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)"><strong>IoCreateFile</strong></a>、 <a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile" data-raw-source="[&lt;strong&gt;ZwCreateFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)"><strong>ZwCreateFile</strong></a>、 <a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntopenfile" data-raw-source="[&lt;strong&gt;ZwOpenFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntopenfile)"><strong>ZwOpenFile</strong></a></p></td>
</tr>
<tr class="even">
<td><p>注册表项</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey" data-raw-source="[&lt;strong&gt;IoOpenDeviceInterfaceRegistryKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)"><strong>IoOpenDeviceInterfaceRegistryKey</strong></a>、 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey" data-raw-source="[&lt;strong&gt;IoOpenDeviceRegistryKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)"><strong>IoOpenDeviceRegistryKey</strong></a>、 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey" data-raw-source="[&lt;strong&gt;ZwCreateKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey)"><strong>ZwCreateKey</strong></a>、 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey" data-raw-source="[&lt;strong&gt;ZwOpenKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey)"><strong>ZwOpenKey</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>线程数</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-pscreatesystemthread" data-raw-source="[&lt;strong&gt;PsCreateSystemThread&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-pscreatesystemthread)"><strong>PsCreateSystemThread</strong></a></p></td>
</tr>
<tr class="even">
<td><p>事件</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesynchronizationevent" data-raw-source="[&lt;strong&gt;IoCreateSynchronizationEvent&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesynchronizationevent)"><strong>IoCreateSynchronizationEvent</strong></a>、 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatenotificationevent" data-raw-source="[&lt;strong&gt;IoCreateNotificationEvent&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatenotificationevent)"> <strong>IoCreateNotificationEvent</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>符号链接</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopensymboliclinkobject" data-raw-source="[&lt;strong&gt;ZwOpenSymbolicLinkObject&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopensymboliclinkobject)"><strong>ZwOpenSymbolicLinkObject</strong></a></p></td>
</tr>
<tr class="even">
<td><p>目录对象</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatedirectoryobject" data-raw-source="[&lt;strong&gt;ZwCreateDirectoryObject&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatedirectoryobject)"><strong>ZwCreateDirectoryObject</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>节对象</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopensection" data-raw-source="[&lt;strong&gt;ZwOpenSection&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopensection)"><strong>ZwOpenSection</strong></a></p></td>
</tr>
</tbody>
</table>

 

当驱动程序不再需要访问该对象时，它将调用 [**ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose) 例程来关闭该句柄。 这适用于上表中列出的所有对象类型。

提供句柄的大多数例程将 [**对象 \_ 属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_object_attributes) 结构作为参数。 此结构可用于为句柄指定属性。

驱动程序可以指定下列句柄属性：

-   OBJ \_ 内核 \_ 句柄

    只能从内核模式访问句柄。

-   OBJ \_ 继承

    当创建句柄时，当前进程的所有子级都将接收该句柄的副本。

-   OBJ \_ 强制 \_ 访问 \_ 检查

    此属性指定系统对句柄执行所有访问检查。 默认情况下，系统会绕过在内核模式下创建的句柄的所有访问检查。

使用 [**InitializeObjectAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/nf-wudfwdm-initializeobjectattributes) 例程在 **对象 \_ 属性** 结构中设置这些属性。

有关验证对象句柄的信息，请参阅 [验证对象句柄失败](failure-to-validate-object-handles.md)。

### <a name="private-object-handles"></a>专用对象句柄

每当驱动程序为其专用使用创建对象句柄时，驱动程序必须指定 OBJ \_ 内核 \_ 句柄特性。 这可确保用户模式应用程序无法访问句柄。

### <a name="shared-object-handles"></a>共享对象句柄

必须仔细编写在内核模式和用户模式之间共享对象句柄的驱动程序，以避免意外创建安全漏洞。 下面是一些指导原则：

1.  在内核模式下创建句柄并将其传递给用户模式，而不是其他方法。 用户模式组件创建并传递给驱动程序的句柄不应受信任。

2.  如果驱动程序必须代表用户模式应用程序操作句柄，请使用 OBJ \_ 强制 \_ 访问 \_ 检查属性来验证应用程序是否具有所需的访问权限。

3.  使用 [**ObReferenceObjectByPointer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer) 将内核模式引用保留在共享句柄上。 否则，如果用户模式组件关闭了句柄，则引用计数将变为零，并且如果驱动程序尝试使用或关闭句柄，系统会崩溃。

如果用户模式应用程序创建一个事件对象，则驱动程序可以安全等待该事件发出信号，但前提是该应用程序通过 IOCTL 将事件对象的句柄传递给驱动程序。 驱动程序必须在创建事件的进程的上下文中处理 IOCTL，并必须通过调用 [**ObReferenceObjectByHandle**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)来验证该句柄是否为事件句柄。


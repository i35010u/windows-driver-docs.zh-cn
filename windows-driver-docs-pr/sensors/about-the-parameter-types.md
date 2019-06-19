---
title: 有关传感器参数类型
description: 关于参数类型
ms.assetid: 392ea7b9-df6f-4d47-9367-a167c0656dd4
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 99848cefd1ad8e9f2de5ffcb46483ee200d2c577
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161433"
---
# <a name="about-sensor-parameter-types"></a>有关传感器参数类型


您应该了解传感器类扩展如何将某些数据类型用作方法参数。 下表介绍了这些数据类型。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>在任务栏的搜索框中键入</th>
<th>参数名称</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdffile" data-raw-source="[IWDFFile](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdffile)">IWDFFile</a></p></td>
<td><p>pClientFile</p></td>
<td><p>此 UMDF COM 接口表示平台将与客户端应用程序相关联的文件对象。 尽管传感器方法调用始终提供此类型作为有效的接口指针，但它被旨在用作应用程序 ID。 包含指针的地址是可以识别客户端应用程序的唯一编号。 请注意，此值是不同于指针本身的地址。 不使用 address-of 运算符 (&) 来检索 id。 使用指针本身。</p>
<p>如果您选择用这个指针来访问基础对象，请记住最初，通过指针调用 AddRef，然后完成后调用 Release。</p></td>
</tr>
<tr class="even">
<td><p><strong>LPWSTR</strong></p></td>
<td><p>pwszSensorID</p></td>
<td><p>此字符串是某个特定传感器驱动程序提供的唯一 ID。 此 ID 必须是唯一的特定设备上的每个传感器。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=131486" data-raw-source="[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)">IPortableDeviceValues</a></p></td>
<td><p>ppDataValues</p>
<p>ppPropertyValues</p>
<p>pPropertiesToSet</p>
<p>ppResults</p></td>
<td><p>此 WPD 接口提供了方便地创建属性包的名称/值对。 <strong>PROPERTYKEY</strong>s 表示名称和<strong>PROPVARIANT</strong>s 表示值。 DDI 使用此接口来设置和检索的值，或为单个值集。</p>
<p>你可以从一种方法来检索此接口或者，如果需要一个新的对象，通过调用使用 CoCreateInstance <strong>CLSID_PortableDeviceValues</strong>。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=131487" data-raw-source="[IPortableDeviceValuesCollection](https://go.microsoft.com/fwlink/p/?linkid=131487)">IPortableDeviceValuesCollection</a></p></td>
<td><p>pEventCollection</p>
<p>ppSensorObjectCollection</p></td>
<td><p>此 WPD 接口包含一系列<a href="https://go.microsoft.com/fwlink/p/?linkid=131486" data-raw-source="[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)">IPortableDeviceValues</a>对象。 使用此接口的 DDI 方法，可提供多个数据集的同时，如多个事件或多个传感器有关的信息。</p>
<p>你可以从一种方法来检索此接口或者，如果需要一个新的对象，通过调用使用 CoCreateInstance <strong>CLSID_PortableDeviceValuesCollection</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=131484" data-raw-source="[IPortableDeviceKeyCollection](https://go.microsoft.com/fwlink/p/?linkid=131484)">IPortableDeviceKeyCollection</a></p></td>
<td><p>pDataFields</p>
<p>pProperties</p>
<p>ppSupportedDataFields</p>
<p>ppSupportedProperties</p></td>
<td><p>此 WPD 接口包含一系列<strong>PROPERTYKEY</strong>s。 这些密钥表示可以存储的属性名称<a href="https://go.microsoft.com/fwlink/p/?linkid=131486" data-raw-source="[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)">IPortableDeviceValues</a>。 DDI 使用此集合对象用于设置和检索的属性名称集或单一名称。</p>
<p>你可以从一种方法来检索此接口或者，如果需要一个新的对象，通过调用使用 CoCreateInstance <strong>CLSID_PortableDeviceKeyCollection</strong>。</p></td>
</tr>
</tbody>
</table>

 

 

 





---
title: 注册表项对象
description: 注册表项对象
ms.assetid: c666f0cc-5a8a-4df8-9c65-08e3b044a08f
keywords:
- helper 对象，WDK 音频，注册表项对象
- 注册表项对象 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcc9cc335f01795f22a5539d98f8b4cc16ee4dc0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830226"
---
# <a name="registry-key-objects"></a>注册表项对象


## <span id="registry_key_objects"></span><span id="REGISTRY_KEY_OBJECTS"></span>


PortCls 系统驱动程序实现[IRegistryKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iregistrykey)接口，以获得微型端口驱动程序的优势。 IRegistryKey 对象表示注册表项。 微型端口驱动程序使用注册表项对象执行以下操作：

-   创建和删除注册表项

-   枚举注册表项

-   查询和设置注册表项

查询注册表项对象以获取有关指定键下的注册表项的信息时，查询可以使用三种格式中的一种来输出信息，其中每种格式都使用不同的键查询结构。 下表显示了\_类枚举值的[**键\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_key_information_class)，这些枚举值指示查询输出的三个键查询结构中的哪一个。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KEY_INFORMATION_CLASS 值</th>
<th align="left">键查询结构</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>KeyBasicInformation</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_key_basic_information" data-raw-source="[&lt;strong&gt;KEY_BASIC_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_key_basic_information)"><strong>KEY_BASIC_INFORMATION</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>KeyFullInformation</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_key_full_information" data-raw-source="[&lt;strong&gt;KEY_FULL_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_key_full_information)"><strong>KEY_FULL_INFORMATION</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>KeyNodeInformation</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_key_node_information" data-raw-source="[&lt;strong&gt;KEY_NODE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_key_node_information)"><strong>KEY_NODE_INFORMATION</strong></a></p></td>
</tr>
</tbody>
</table>

 

若要打开现有的注册表项或创建一个新的注册表项，适配器驱动程序可以调用[**PcNewRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewregistrykey)函数，而微型端口驱动程序可以调用端口驱动程序的[**IPort：： NewRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-newregistrykey)方法。 这两个调用是相似的，只不过**PcNewRegistryKey**函数需要两个附加参数*DeviceObject*和*SubDevice*。 有关详细信息，请参阅**PcNewRegistryKey**。

当微型端口驱动程序创建新的[IRegistryKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iregistrykey)对象时，对象会打开现有子项，如果不存在，则创建新的注册表子项。 在任一情况下，注册表项对象都将句柄存储到密钥。 以后释放该对象并将其引用计数减为零时，该对象会自动关闭其对该键的句柄。

[IRegistryKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iregistrykey)接口支持以下方法：

[**IRegistryKey：:D eleteKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iregistrykey-deletekey)

[**IRegistryKey::EnumerateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iregistrykey-enumeratekey)

[**IRegistryKey::EnumerateValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iregistrykey-enumeratevaluekey)

[**IRegistryKey::NewSubKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iregistrykey-newsubkey)

[**IRegistryKey：：查询密钥**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iregistrykey-querykey)

[**IRegistryKey::QueryRegistryValues**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iregistrykey-queryregistryvalues)

[**IRegistryKey::QueryValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iregistrykey-queryvaluekey)

[**IRegistryKey::SetValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iregistrykey-setvaluekey)

 

 





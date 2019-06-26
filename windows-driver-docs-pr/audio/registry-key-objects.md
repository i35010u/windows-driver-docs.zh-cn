---
title: 注册表项对象
description: 注册表项对象
ms.assetid: c666f0cc-5a8a-4df8-9c65-08e3b044a08f
keywords:
- 帮助程序对象 WDK 音频，注册表项对象
- 注册表项对象 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0c5a8bf902385b163568e8c35eece77fa41800c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355274"
---
# <a name="registry-key-objects"></a>注册表项对象


## <span id="registry_key_objects"></span><span id="REGISTRY_KEY_OBJECTS"></span>


PortCls 系统驱动程序实现[IRegistryKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iregistrykey)为了方便微型端口驱动程序的接口。 IRegistryKey 对象表示的注册表项。 微型端口驱动程序使用注册表项对象执行以下操作：

-   创建和删除注册表项

-   枚举注册表项

-   查询和设置注册表项

在查询时指定的密钥下的注册表项有关的信息的注册表项对象，该查询可以输出某个三种格式，其中每个使用不同的键查询结构中的信息。 下表显示[**密钥\_信息\_类**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_key_information_class)枚举值，用于指示这三个键查询结构是由查询的输出。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_key_basic_information" data-raw-source="[&lt;strong&gt;KEY_BASIC_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_key_basic_information)"><strong>KEY_BASIC_INFORMATION</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>KeyFullInformation</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_key_full_information" data-raw-source="[&lt;strong&gt;KEY_FULL_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_key_full_information)"><strong>KEY_FULL_INFORMATION</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>KeyNodeInformation</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_key_node_information" data-raw-source="[&lt;strong&gt;KEY_NODE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_key_node_information)"><strong>KEY_NODE_INFORMATION</strong></a></p></td>
</tr>
</tbody>
</table>

 

若要打开现有的注册表项或创建新的注册表项，适配器驱动程序可以调用[ **PcNewRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewregistrykey)函数，并且微型端口驱动程序可以调用端口驱动程序的[ **IPort::NewRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iport-newregistrykey)方法。 两个调用都是类似，只不过**PcNewRegistryKey**函数要求两个其他参数*DeviceObject*并*子*。 有关详细信息，请参阅**PcNewRegistryKey**。

微型端口驱动程序时创建一个新[IRegistryKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iregistrykey)对象，该对象将打开一个现有子项或创建一个新的注册表子项，如果不存在。 在任一情况下，注册表项对象存储到密钥句柄。 更高版本发布时该对象和其引用计数递减到零，该对象会自动关闭其密钥句柄。

[IRegistryKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iregistrykey)接口支持以下方法：

[**IRegistryKey::DeleteKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iregistrykey-deletekey)

[**IRegistryKey::EnumerateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iregistrykey-enumeratekey)

[**IRegistryKey::EnumerateValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iregistrykey-enumeratevaluekey)

[**IRegistryKey::NewSubKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iregistrykey-newsubkey)

[**IRegistryKey::QueryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iregistrykey-querykey)

[**IRegistryKey::QueryRegistryValues**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iregistrykey-queryregistryvalues)

[**IRegistryKey::QueryValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iregistrykey-queryvaluekey)

[**IRegistryKey::SetValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iregistrykey-setvaluekey)

 

 





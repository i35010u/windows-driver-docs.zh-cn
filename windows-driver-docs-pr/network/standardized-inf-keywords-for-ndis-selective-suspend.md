---
title: NDIS 选择性挂起的标准化 INF 关键字
description: NDIS 选择性挂起的标准化 INF 关键字
ms.assetid: A45EE23D-1C60-4DA4-82A5-89DB5CE48E21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24e0d1489e2117ec59ccdf9ed0a05e8839d73c10
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378638"
---
# <a name="standardized-inf-keywords-for-ndis-selective-suspend"></a>NDIS 选择性挂起的标准化 INF 关键字


以下的标准化的 INF 关键字定义以启用、 禁用和配置参数的 NDIS 选择性挂起微型端口驱动程序：

[ **\*SelectiveSuspend** INF 关键字](#selectivesuspend-inf-keyword)

[ **\*SSIdleTimeout** INF 关键字](#ssidletimeout-inf-keyword)

[ **\*SSIdleTimeoutScreenOff** INF 关键字](#ssidletimeoutscreenoff-inf-keyword)


有关标准化 INF 关键字的详细信息，请参阅[为网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

## <a name="selectivesuspend-inf-keyword"></a>\*SelectiveSuspend INF 关键字


必须指定的支持 NDIS 选择性挂起的微型端口驱动程序的 INF 文件 **\*SelectiveSuspend** 标准化 INF 关键字。 安装该驱动程序后，管理员可以更新 **\*SelectiveSuspend** 中的关键字值**高级**网络适配器的属性页。 有关高级属性的详细信息，请参阅[的高级属性页指定配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

**请注意**   中进行更改后的微型端口驱动程序将自动重启**高级**适配器属性页。

 

**\*SelectiveSuspend** INF 关键字是一个枚举的关键字。 下表描述了可能 INF 条目 **\*SelectiveSuspend** INF 关键字。 此表中的列描述枚举关键字的以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须在 INF 文件中指定的关键字的名称。 此名称也会出现在注册表 **NDI\\params\\** 关键网络适配器。

<a href="" id="paramdesc"></a>ParamDesc  
显示文本与 SubkeyName 相关联。

**请注意**   独立硬件供应商 (IHV) 可以为 SubkeyName 定义描述性文本。

 

<a href="" id="value"></a>值  
枚举的整数值与列表中每个 SubkeyName 相关联。

<a href="" id="enumdesc"></a>EnumDesc  
将出现在每个值与相关联的显示文本**高级**属性页。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">ReplTest1</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>*SelectiveSuspend</strong></p></td>
<td align="left"><p>选择性挂起</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
</tbody>
</table>

 

微型端口驱动程序必须检查 **\*SelectiveSuspend** 之前的 NDIS 选择性挂起，也会公布其支持在注册表中的关键字值。 如果 **\*SelectiveSuspend** 关键字的值为零、 微型端口必须不播发任何支持选择性挂起功能。 有关详细信息，请参阅[报告 NDIS 选择性挂起功能](reporting-ndis-selective-suspend-capabilities.md)。

## <a name="ssidletimeout-inf-keyword"></a>\*SSIdleTimeout INF 关键字


INF 文件微型端口驱动程序支持 NDIS 选择性挂起，应指定可选 **\*SSIdleTimeout** 标准化 INF 关键字。 此关键字指定以秒为单位的空闲超时时期。 如果 NDIS 超过一段不检测网络适配器上的任何活动 **\*SSIdleTimeout** 值、 NDIS 启动选择性，则挂起通过调用微型端口驱动程序的操作[ *MiniportIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_idle_notification)处理程序函数。

安装该驱动程序后，管理员可以更新 **\*SSIdleTimeout** 中的关键字值**高级**网络适配器的属性页。 有关高级属性的详细信息，请参阅[的高级属性页指定配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

**请注意**  微型端口驱动程序将自动重启后，适配器的高级的属性页中进行更改。

 

**\*SSIdleTimeout** INF 关键字是一个数值 (**Int**) 关键字。 下表描述了可能 INF 条目 **\*SSIdleTimeout** INF 关键字。 列的表中描述的以下特性**Int**关键字：

<a href="" id="subkeyname"></a>SubkeyName  
必须在 INF 文件中指定的关键字的名称。 此名称也会出现在注册表 **NDI\\params\\** 关键网络适配器。

<a href="" id="paramdesc"></a>ParamDesc  
显示文本与 SubkeyName 相关联。

**请注意**   独立硬件供应商 (IHV) 可以为 SubkeyName 定义描述性文本。

 

<a href="" id="default-value"></a>默认值  
整数默认值。

<a href="" id="minimum-value"></a>最小值  
允许整数的最小值。

<a href="" id="maximum-value"></a>最大值  
允许整数的最大值。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">默认值</th>
<th align="left">最小值</th>
<th align="left">最大值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>*SSIdleTimeout</strong></p></td>
<td align="left"><p>选择性挂起中以秒为单位的空闲超时</p></td>
<td align="left"><p>5</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>60</p></td>
</tr>
</tbody>
</table>

 

**请注意**   NDIS 读取的值 **\*SSIdleTimeout** 其驱动程序支持 NDIS 选择性的网络适配器的每个实例的标准化的 INF 关键字挂起。 微型端口驱动程序不应读取此关键字。

 

NDIS 测量使用计时器是精确到 30%的空闲超时 **\*SSIdleTimeout**值。 例如，如果 **\*SSIdleTimeout** 值为 10，适配器挂起 NDIS 首先检测适配器处于空闲状态后 10 到 13 秒之间。


## <a name="ssidletimeoutscreenoff-inf-keyword"></a>\*SSIdleTimeoutScreenOff INF 关键字


INF 文件微型端口驱动程序支持 NDIS 选择性挂起，应指定可选 **\*SSIdleTimeoutScreenOff** 标准化 INF 关键字。 此关键字指定以秒为单位的空闲超时时期，并在屏幕处于关闭状态时才适用。 如果 NDIS 超过一段不检测网络适配器上的任何活动 **\*SSIdleTimeoutScreenOff** 屏幕处于关闭状态后值、 NDIS 启动选择性，则挂起通过调用微型端口操作驱动程序的[ *MiniportIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_idle_notification)处理程序函数。

安装该驱动程序后，管理员可以更新 **\*SSIdleTimeoutScreenOff** 中的关键字值**高级**网络适配器的属性页。 有关高级属性的详细信息，请参阅[的高级属性页指定配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

**请注意**微型端口驱动程序将自动重启后，适配器的高级的属性页中进行更改。

 

**\*SSIdleTimeoutScreenOff** INF 关键字是一个数值 (**Int**) 关键字。 下表描述了可能 INF 条目 **\*SSIdleTimeoutScreenOff** INF 关键字。 列的表中描述的以下特性**Int**关键字：

<a href="" id="subkeyname"></a>SubkeyName  
必须在 INF 文件中指定的关键字的名称。 此名称也会出现在注册表 **NDI\\params\\** 关键网络适配器。

<a href="" id="paramdesc"></a>ParamDesc  
显示文本与 SubkeyName 相关联。

**请注意**独立硬件供应商 (IHV) 可以为 SubkeyName 定义描述性文本。

 

<a href="" id="default-value"></a>默认值  
整数默认值。

<a href="" id="minimum-value"></a>最小值  
允许整数的最小值。

<a href="" id="maximum-value"></a>最大值  
允许整数的最大值。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">默认值</th>
<th align="left">最小值</th>
<th align="left">最大值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>*SSIdleTimeoutScreenOff</strong></p></td>
<td align="left"><p>选择性挂起中以秒为单位的空闲超时</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>60</p></td>
</tr>
</tbody>
</table>

 

**请注意**NDIS 读取的值 **\*SSIdleTimeoutScreenOff** 其驱动程序支持 NDIS 选择性的网络适配器的每个实例的标准化的 INF 关键字挂起。 微型端口驱动程序不应读取此关键字。

**请注意**的最大值是仅用于测试目的。 HLK 认证测试显式将检查并失败值是否大于 5。

 
NDIS 测量使用计时器是精确到 30%的空闲超时 **\*SSIdleTimeoutScreenOff** 值。 例如，如果 **\*SSIdleTimeoutScreenOff** 值为 5，适配器挂起 NDIS 首先检测适配器处于空闲状态后的 5 到 6.5 秒之间。


 






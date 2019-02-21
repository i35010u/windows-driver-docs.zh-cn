---
title: UPS 状态注册表项
description: UPS 微型驱动程序必须设置某些 UPS 状态注册表项
ms.assetid: c24ef185-ba8d-4cfd-9d33-b70682905f00
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 874a732c925e8663acd04de22c970860f8dba5f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520686"
---
# <a name="upsstatus-registry-entries"></a>UPS\\状态注册表项


## <span id="ddk_ups_status_registry_entries_kg"></span><span id="DDK_UPS_STATUS_REGISTRY_ENTRIES_KG"></span>


以下注册表项下**UPS**\\**状态**密钥，必须由 UPS 微型驱动程序设置。

### <a name="span-idbatterycapacityspanspan-idbatterycapacityspanspan-idbatterycapacityspanbatterycapacity"></a><span id="BatteryCapacity"></span><span id="batterycapacity"></span><span id="BATTERYCAPACITY"></span>BatteryCapacity

<span id="Value_Name"></span><span id="value_name"></span><span id="VALUE_NAME"></span>值名称  
**BatteryCapacity**

<span id="Value_Type"></span><span id="value_type"></span><span id="VALUE_TYPE"></span>值类型  
REG\_DWORD

<span id="Value"></span><span id="value"></span><span id="VALUE"></span>值  
UPS 中剩余电池电量的百分比。 此百分比表示为 0 到 100 的范围中的值。 （显示的值舍入到最接近的整数。）

<span id="Default_Value"></span><span id="default_value"></span><span id="DEFAULT_VALUE"></span>默认值  
0

### <a name="span-idbatterystatusspanspan-idbatterystatusspanspan-idbatterystatusspanbatterystatus"></a><span id="BatteryStatus"></span><span id="batterystatus"></span><span id="BATTERYSTATUS"></span>BatteryStatus

<span id="Value_Name"></span><span id="value_name"></span><span id="VALUE_NAME"></span>值名称  
**BatteryStatus**

<span id="Value_Type"></span><span id="value_type"></span><span id="VALUE_TYPE"></span>值类型  
REG\_DWORD

<span id="Value"></span><span id="value"></span><span id="VALUE"></span>值  
UPS 电池的当前状态。 下表列出了值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>电池状态是未知的。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>电池是确定。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>需要更换电池。</p></td>
</tr>
</tbody>
</table>

 

<span id="Default_Value"></span><span id="default_value"></span><span id="DEFAULT_VALUE"></span>默认值  
0

### <a name="span-idcommstatusspanspan-idcommstatusspanspan-idcommstatusspancommstatus"></a><span id="CommStatus"></span><span id="commstatus"></span><span id="COMMSTATUS"></span>CommStatus

<span id="Value_Name"></span><span id="value_name"></span><span id="VALUE_NAME"></span>值名称  
**CommStatus**

<span id="Value_Type"></span><span id="value_type"></span><span id="VALUE_TYPE"></span>值类型  
REG\_DWORD

<span id="Value"></span><span id="value"></span><span id="VALUE"></span>值  
UPS 的通信路径的状态。 下表列出了值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>UPS 的通信路径是未知的。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>UPS 的通信路径是确定。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>UPS 的通信路径已丢失。</p></td>
</tr>
</tbody>
</table>

 

<span id="Default_Value"></span><span id="default_value"></span><span id="DEFAULT_VALUE"></span>默认值  
1

### <a name="span-idfirmwarerevspanspan-idfirmwarerevspanspan-idfirmwarerevspanfirmwarerev"></a><span id="FirmwareRev"></span><span id="firmwarerev"></span><span id="FIRMWAREREV"></span>FirmwareRev

<span id="Value_Name"></span><span id="value_name"></span><span id="VALUE_NAME"></span>值名称  
**FirmwareRev**

<span id="Value_Type"></span><span id="value_type"></span><span id="VALUE_TYPE"></span>值类型  
REG\_SZ

<span id="Value"></span><span id="value"></span><span id="VALUE"></span>值  
报告可显示字符串形式的 UPS 固件修订版本。

<span id="Default_Value_"></span><span id="default_value_"></span><span id="DEFAULT_VALUE_"></span>默认值：  
""

### <a name="span-idserialnumberspanspan-idserialnumberspanspan-idserialnumberspanserialnumber"></a><span id="SerialNumber"></span><span id="serialnumber"></span><span id="SERIALNUMBER"></span>SerialNumber

<span id="Value_Name"></span><span id="value_name"></span><span id="VALUE_NAME"></span>值名称  
**SerialNumber**

<span id="Value_Type"></span><span id="value_type"></span><span id="VALUE_TYPE"></span>值类型  
REG\_SZ

<span id="Value"></span><span id="value"></span><span id="VALUE"></span>值  
报告可显示字符串 UPS 序列号。

<span id="Default_Value_"></span><span id="default_value_"></span><span id="DEFAULT_VALUE_"></span>默认值：  
""

### <a name="span-idtotalupsruntimespanspan-idtotalupsruntimespanspan-idtotalupsruntimespantotalupsruntime"></a><span id="TotalUPSRuntime"></span><span id="totalupsruntime"></span><span id="TOTALUPSRUNTIME"></span>TotalUPSRuntime

<span id="Value_Name"></span><span id="value_name"></span><span id="VALUE_NAME"></span>值名称  
**TotalUPSRuntime**

<span id="Value_Type"></span><span id="value_type"></span><span id="VALUE_TYPE"></span>值类型  
REG\_DWORD

<span id="Value"></span><span id="value"></span><span id="VALUE"></span>值  
剩余 UPS 运行的时间，以分钟为单位。

<span id="Default_Value"></span><span id="default_value"></span><span id="DEFAULT_VALUE"></span>默认值  
0

### <a name="span-idutilitypowerstatusspanspan-idutilitypowerstatusspanspan-idutilitypowerstatusspanutilitypowerstatus"></a><span id="UtilityPowerStatus"></span><span id="utilitypowerstatus"></span><span id="UTILITYPOWERSTATUS"></span>UtilityPowerStatus

<span id="Value_Name"></span><span id="value_name"></span><span id="VALUE_NAME"></span>值名称  
**UtilityPowerStatus**

<span id="Value_Type"></span><span id="value_type"></span><span id="VALUE_TYPE"></span>值类型  
REG\_DWORD

<span id="Value_"></span><span id="value_"></span><span id="VALUE_"></span>值：  
报告到 UPS 实用程序提供电源的状态。 下表列出了值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>实用程序提供电源的状态是未知的。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>实用程序提供电源是确定。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>出现电源故障。</p></td>
</tr>
</tbody>
</table>

 

<span id="Default_Value"></span><span id="default_value"></span><span id="DEFAULT_VALUE"></span>默认值  
0

 

 





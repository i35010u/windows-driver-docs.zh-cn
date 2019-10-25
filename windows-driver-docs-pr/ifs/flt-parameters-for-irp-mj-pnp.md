---
title: FLT_PARAMETERS for IRP_MJ_PNP union
description: 当 FLT 的 MajorFunction 字段\_IO\_参数\_操作的块结构为 IRP\_MJ\_PNP 时使用的联合组件。
ms.assetid: d3ce893b-f113-4c50-8f52-30c7ced25ae0
keywords:
- FLT_PARAMETERS for IRP_MJ_PNP union 可安装的文件系统驱动程序
- FLT_PARAMETERS 可安装的可安装文件系统驱动程序
- PFLT_PARAMETERS 联合指针可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FLT_PARAMETERS
api_location:
- fltkernel.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3616ed735b800711ea85c3581e016ed3ed589391
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841369"
---
# <a name="flt_parameters-for-irp_mj_pnp-union"></a>用于 IRP\_MJ\_PNP 联合的 FLT\_参数


当 FLT 的**MajorFunction**字段[ **\_IO\_参数\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)操作的块结构为[**IRP\_MJ\_PNP**](irp-mj-pnp.md)时使用的联合组件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...   ;
  union {
    struct  StartDevice;
    struct  QueryDeviceRelations;
    struct  QueryInterface;
    struct  DeviceCapabilities;
    struct  FilterResourceRequirements;
    struct  ReadWriteConfig;
    struct  SetLock;
    struct  QueryId;
    struct  QueryDeviceText;
    struct  UsageNotification;
  } Pnp;
  ...   ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**Pnp-x**  
**StartDevice**  
用于 IRP\_MN\_启动\_设备操作的联合组件。 有关此操作的参数的详细信息，请参阅[**IRP\_MN\_START\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)的参考条目。

**QueryDeviceRelations**  
用于 IRP 的联合组件\_MN\_QUERY\_设备\_关系操作。 有关此操作的参数的详细信息，请参阅[**IRP\_MN\_QUERY\_设备\_关系**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)的参考条目。

**QueryInterface**  
用于 IRP\_MN\_QUERY\_INTERFACE 操作的联合组件。 有关此操作的参数的详细信息，请参阅[**IRP\_MN\_QUERY\_接口**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)的参考条目。

**DeviceCapabilities**  
用于 IRP\_MN\_QUERY\_功能操作的联合组件。 有关此操作的参数的详细信息，请参阅[**IRP\_MN\_QUERY\_功能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)的参考条目。

**FilterResourceRequirements**  
用于 IRP\_MN 的联合组件\_筛选\_资源\_要求操作。 有关此操作的参数的详细信息，请参阅[**IRP\_MN\_筛选器的参考条目\_资源\_要求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)。

**ReadWriteConfig**  
用于 IRP\_MN 的联合组件\_读取\_CONFIG 和 IRP\_MN\_写入\_配置操作。 有关此操作的参数的详细信息，请参阅[**IRP\_MN 的参考条目\_读取\_配置**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-read-config)和[**IRP\_MN\_写入\_配置**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-write-config)。

**SetLock**  
用于 IRP\_MN\_集\_锁定操作的联合组件。 有关此操作的参数的详细信息，请参阅[**IRP\_MN\_集\_锁定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-lock)的参考条目。

**QueryId**  
用于 IRP\_MN\_QUERY\_ID 操作的联合组件。 有关此操作的参数的详细信息，请参阅[**IRP\_MN\_QUERY\_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)的引用条目。

**QueryDeviceText**  
用于 IRP 的联合组件\_MN\_QUERY\_设备\_文本操作。 有关此操作的参数的详细信息，请参阅[**IRP\_MN\_QUERY 的参考条目\_设备\_文本**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-text)。

**UsageNotification**  
用于 IRP\_MN\_设备\_使用\_通知操作的联合组件。 有关此操作的参数的详细信息，请参阅[**IRP\_MN\_设备的参考条目\_使用情况\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)。

<a name="remarks"></a>备注
-------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)操作的[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构包含回调数据表示的基于 IRP 的即插即用（PNP）操作（[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)）的参数构造. 它包含在[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构。

IRP\_MJ\_PNP 操作是基于 IRP 的操作。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Fltkernel （包括 Fltkernel）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_\_FASTIO\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_\_FS\_筛选器\_操作**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_\_IRP\_操作**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

[**IRP\_MJ\_PNP （WDK 内核模式驱动程序体系结构参考）** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)

[**IRP\_MN\_设备\_使用情况\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)

[**IRP\_MN\_筛选器\_资源\_要求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)

[**IRP\_MN\_查询\_功能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)

[**IRP\_MN\_查询\_设备\_关系**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)

[**IRP\_MN\_查询\_设备\_文本**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-text)

[**IRP\_MN\_查询\_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)

[**IRP\_MN\_QUERY\_接口**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)

[**IRP\_MN\_读取\_配置**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-read-config)

[**IRP\_MN\_设置\_锁**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-lock)

[**IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)

[**IRP\_MN\_写入\_配置**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-write-config)

 

 







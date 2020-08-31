---
title: IRP_MJ_PNP 联合的 FLT_PARAMETERS
description: 操作的 FLT \_ IO \_ 参数块结构的 MajorFunction 字段 \_ 为 IRP \_ MJ \_ PNP 时使用的联合组件。
ms.assetid: d3ce893b-f113-4c50-8f52-30c7ced25ae0
keywords:
- IRP_MJ_PNP 联合可安装文件系统驱动程序的 FLT_PARAMETERS
- FLT_PARAMETERS 联合可安装文件系统驱动程序
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
ms.openlocfilehash: 931418f3afb7aa2f269252d7c9e6d41652ea1c48
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063426"
---
# <a name="flt_parameters-for-irp_mj_pnp-union"></a>\_IRP \_ MJ \_ PNP 联合的 FLT 参数


操作的[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**MajorFunction**字段为[**IRP \_ MJ \_ PNP**](irp-mj-pnp.md)时使用的联合组件。

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
用于 IRP \_ MN \_ 启动设备操作的联合组件 \_ 。 有关此操作的参数的详细信息，请参阅 [**IRP \_ MN \_ START \_ 设备**](../kernel/irp-mn-start-device.md)的参考条目。

**QueryDeviceRelations**  
用于 IRP \_ MN \_ 查询 \_ 设备 \_ 关系操作的联合组件。 有关此操作的参数的详细信息，请参阅 [**IRP \_ MN \_ 查询 \_ 设备 \_ 关系**](../kernel/irp-mn-query-device-relations.md)的参考条目。

**QueryInterface**  
用于 IRP \_ MN \_ 查询接口操作的联合组件 \_ 。 有关此操作的参数的详细信息，请参阅 [**IRP \_ MN \_ QUERY \_ INTERFACE**](../kernel/irp-mn-query-interface.md)的 reference 条目。

**DeviceCapabilities**  
用于 IRP \_ MN \_ 查询功能操作的联合组件 \_ 。 有关此操作的参数的详细信息，请参阅 [**IRP \_ MN \_ 查询 \_ 功能**](../kernel/irp-mn-query-capabilities.md)的参考条目。

**FilterResourceRequirements**  
用于 IRP \_ MN \_ FILTER \_ 资源 \_ 需求操作的联合组件。 有关此操作的参数的详细信息，请参阅 [**IRP \_ MN \_ 筛选器 \_ 资源 \_ 要求**](../kernel/irp-mn-filter-resource-requirements.md)的参考条目。

**ReadWriteConfig**  
用于 IRP \_ MN \_ READ \_ config 和 irp \_ MN \_ 写入 \_ 配置操作的联合组件。 有关此操作的参数的详细信息，请参阅 [**irp \_ MN \_ READ \_ config**](../kernel/irp-mn-read-config.md) 和 [**irp \_ MN \_ WRITE \_ config**](../kernel/irp-mn-write-config.md)的参考条目。

**SetLock**  
用于 IRP \_ MN \_ SET LOCK 操作的联合组件 \_ 。 有关此操作的参数的详细信息，请参阅 [**IRP \_ MN \_ SET \_ LOCK**](../kernel/irp-mn-set-lock.md)的参考条目。

**QueryId**  
用于 IRP \_ MN \_ 查询 ID 操作的联合组件 \_ 。 有关此操作的参数的详细信息，请参阅 [**IRP \_ MN \_ QUERY \_ ID**](../kernel/irp-mn-query-id.md)的引用条目。

**QueryDeviceText**  
用于 IRP \_ MN \_ 查询 \_ 设备 \_ 文本操作的联合组件。 有关此操作的参数的详细信息，请参阅 [**IRP \_ MN \_ 查询 \_ 设备 \_ 文本**](../kernel/irp-mn-query-device-text.md)的参考条目。

**UsageNotification**  
用于 IRP \_ MN \_ 设备 \_ 使用情况 \_ 通知操作的联合组件。 有关此操作的参数的详细信息，请参阅 [**IRP \_ MN \_ 设备 \_ 使用 \_ 通知**](../kernel/irp-mn-device-usage-notification.md)的参考条目。

<a name="remarks"></a>备注
-------

[**Irp \_ MJ \_ Pnp**](irp-mj-pnp.md)操作的[**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构包含 (PNP) 操作所表示的基于 IRP 即插即用 PNP 操作的参数， ([**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 结构。 它包含在 [**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block) 结构中。

IRP \_ MJ \_ PNP 操作是基于 IRP 的操作。

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
<td align="left">Fltkernel (包含 Fltkernel) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT \_ 是 \_ FASTIO \_ 操作**](/windows-hardware/drivers/ddi/index)

[**FLT \_ 为 \_ FS \_ 筛选器 \_ 操作**](/previous-versions/ff544648(v=vs.85))

[**FLT \_ 是 \_ IRP \_ 操作**](/previous-versions/ff544654(v=vs.85))

[**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP \_ MJ \_ PNP**](irp-mj-pnp.md)

[**IRP \_ MJ \_ PNP (WDK 内核模式驱动程序体系结构参考) **](../kernel/irp-mj-pnp.md)

[**IRP \_ MN \_ 设备 \_ 使用 \_ 通知**](../kernel/irp-mn-device-usage-notification.md)

[**IRP \_ MN \_ 筛选器 \_ 资源 \_ 要求**](../kernel/irp-mn-filter-resource-requirements.md)

[**IRP \_ MN \_ 查询 \_ 功能**](../kernel/irp-mn-query-capabilities.md)

[**IRP \_ MN \_ 查询 \_ 设备 \_ 关系**](../kernel/irp-mn-query-device-relations.md)

[**IRP \_ MN \_ 查询 \_ 设备 \_ 文本**](../kernel/irp-mn-query-device-text.md)

[**IRP \_ MN \_ 查询 \_ ID**](../kernel/irp-mn-query-id.md)

[**IRP \_ MN \_ 查询 \_ 接口**](../kernel/irp-mn-query-interface.md)

[**IRP \_ MN \_ 读取 \_ 配置**](../kernel/irp-mn-read-config.md)

[**IRP \_ MN \_ 设置 \_ 锁定**](../kernel/irp-mn-set-lock.md)

[**IRP \_ MN \_ 启动 \_ 设备**](../kernel/irp-mn-start-device.md)

[**IRP \_ MN \_ 写入 \_ 配置**](../kernel/irp-mn-write-config.md)

 


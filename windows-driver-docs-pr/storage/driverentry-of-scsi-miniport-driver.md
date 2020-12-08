---
title: DriverEntry SCSI 微型端口驱动程序例程
description: 每个微型端口驱动程序必须有一个显式命名为 DriverEntry 的例程才能加载。请注意，SCSI 端口驱动程序和 SCSI 微型端口驱动程序模型可能会在将来更改或不可用。
keywords:
- DriverEntry 例程存储设备
topic_type:
- apiref
api_name:
- DriverEntry
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 05e25dae50077000d903189e92ae47d92c193924
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804669"
---
# <a name="driverentry-of-scsi-miniport-driver-routine"></a>DriverEntry SCSI 微型端口驱动程序例程


每个微型端口驱动程序必须有一个显式命名为 **DriverEntry** 的例程才能加载。

> [!NOTE]
> SCSI 端口驱动程序和 SCSI 微型端口驱动程序模型可能会在将来更改或不可用。 相反，我们建议使用 [storport 驱动](./storport-driver-overview.md) 程序和 [storport 微型端口](./storport-miniport-drivers.md) 驱动程序模型。

 

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
ULONG DriverEntry(
  _In_ PVOID Argument1,
  _In_ PVOID Argument2
);
```

<a name="parameters"></a>参数
----------

*Argument1* \[中\]  
是一个指针，微型端口驱动程序必须调用 **ScsiPortInitialize**。

*Argument2* \[中\]  
是一个指针，微型端口驱动程序必须调用 **ScsiPortInitialize**。

<a name="return-value"></a>返回值
------------

**DriverEntry** 返回 **ScsiPortInitialize** 返回的值。 如果多次调用 **ScsiPortInitialize** ，则 **DriverEntry** 将返回 **ScsiPortInitialize** 返回的最小值。

<a name="remarks"></a>备注
-------

微型端口驱动程序的 **DriverEntry** 例程在堆栈上分配内存，并 \_ 使用零初始化 HW 初始化 \_ 数据结构。 **DriverEntry** 在 \_ \_ 用适用于) 微型端口驱动程序支持的 HBA (的值初始化之前，DriverEntry 的所有成员必须为零。

**DriverEntry** 应将 **HwInitializationDataSize** 成员设置为 **sizeof** (HW \_ 初始化 \_ 数据) ，以指示其所使用的结构的版本，并为其 HBA () 初始化所有成员。

接下来， **DriverEntry** 调用 **ScsiPortInitialize**。 如果微型端口驱动程序支持可以连接到多种类型 i/o 总线（例如 **MicroChannel** 和 **Isa** 类型总线）的 HBA () ，则它应为每种类型的 i/o 总线调用 **ScsiPortInitialize** 一次。 此类微型端口驱动程序必须从 **DriverEntry** 例程返回对 **ScsiPortInitialize** 的调用返回的最小值。 小型小型驱动程序编写器不会假设 **ScsiPortInitialize** 返回的值。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/srb/ns-srb-_hw_initialization_data)

[*HwScsiFindAdapter*](/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))

[**ScsiPortInitialize**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize)


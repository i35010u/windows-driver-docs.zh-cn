---
title: DriverEntry 的 SCSI 微型端口驱动程序例程
description: 每个微型端口驱动程序必须具有显式命名以便加载 DriverEntry 例程。请注意 SCSI 端口驱动程序和 SCSI 微型端口驱动程序模型可能被修改或不可用在将来。
ms.assetid: dda79363-06a9-4902-8e04-186293b6c9d4
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
ms.openlocfilehash: 57dc75fa879d3ec79e5471104064cf387e8990b3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566208"
---
# <a name="driverentry-of-scsi-miniport-driver-routine"></a>DriverEntry 的 SCSI 微型端口驱动程序例程


每个微型端口驱动程序必须具有显式命名的例程**DriverEntry**才能加载。

&gt; \[!请注意\] &gt; SCSI 端口驱动程序和 SCSI 微型端口驱动程序模型可能被修改或不可用在将来。 相反，我们建议使用[Storport 驱动程序](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-driver)并[Storport 微型端口](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-miniport-drivers)驱动程序模型。

 

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
ULONG DriverEntry(
  _In_ PVOID Argument1,
  _In_ PVOID Argument2
);
```

<a name="parameters"></a>Parameters
----------

*Argument1* \[中\]  
是一个指针，微型端口驱动程序必须调用与其**ScsiPortInitialize**。

*Argument2* \[中\]  
是一个指针，微型端口驱动程序必须调用与其**ScsiPortInitialize**。

<a name="return-value"></a>返回值
------------

**DriverEntry**返回的值将返回**ScsiPortInitialize**。 如果它调用**ScsiPortInitialize**不止一次**DriverEntry**返回返回的最小值**ScsiPortInitialize**。

<a name="remarks"></a>备注
-------

微型端口驱动程序**DriverEntry**例程在堆栈上分配内存并初始化 HW\_初始化\_用零的数据结构。 **DriverEntry**必须为零的 HW 中的所有成员\_初始化\_再使用适合的 HBA 微型端口驱动程序的值初始化的数据结构支持。

**DriverEntry**应设置**HwInitializationDataSize**成员添加到**sizeof**(HW\_初始化\_数据) 以指示此结构的版本它是使用，以及初始化为其 HBA(s) 适当的所有成员。

下一步， **DriverEntry**调用**ScsiPortInitialize**。 微型端口驱动程序是否支持多个类型的 I/O 总线，如上可以连接的 HBA(s)**微通道**并**Isa**键入总线，则应调用**ScsiPortInitialize**每种类型的 I/O 总线的一次。 这样的微型端口驱动程序必须返回到其调用返回的最小值**ScsiPortInitialize**从**DriverEntry**例程。 微型端口驱动程序编写器可以作出任何假设返回的值**ScsiPortInitialize**。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**HW\_INITIALIZATION\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff557456)

[*HwScsiFindAdapter*](https://msdn.microsoft.com/library/windows/hardware/ff557300)

[**ScsiPortInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff564645)

 

 







---
title: DriverEntry SCSI 微型端口驱动程序例程
description: 每个微型端口驱动程序必须有一个显式命名为 DriverEntry 的例程才能加载。请注意，SCSI 端口驱动程序和 SCSI 微型端口驱动程序模型可能会在将来更改或不可用。
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
ms.openlocfilehash: 2e3bd556f6cfd74c3ce63afb4ab3b54764bef214
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845172"
---
# <a name="driverentry-of-scsi-miniport-driver-routine"></a>DriverEntry SCSI 微型端口驱动程序例程


每个微型端口驱动程序必须有一个显式命名为**DriverEntry**的例程才能加载。

&gt; \[！请注意\] &gt; SCSI 端口驱动程序和 SCSI 微型端口驱动程序模型在将来可能会更改或不可用。 相反，我们建议使用[storport 驱动](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)程序和[storport 微型端口](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)驱动程序模型。

 

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
ULONG DriverEntry(
  _In_ PVOID Argument1,
  _In_ PVOID Argument2
);
```

<a name="parameters"></a>参数
----------

\] 中的*Argument1* \[  
是一个指针，微型端口驱动程序必须调用**ScsiPortInitialize**。

\] 中的*Argument2* \[  
是一个指针，微型端口驱动程序必须调用**ScsiPortInitialize**。

<a name="return-value"></a>返回值
------------

**DriverEntry**返回**ScsiPortInitialize**返回的值。 如果多次调用**ScsiPortInitialize** ，则**DriverEntry**将返回**ScsiPortInitialize**返回的最小值。

<a name="remarks"></a>备注
-------

微型端口驱动程序的**DriverEntry**例程在堆栈上分配内存，并使用零\_数据结构初始化 HW\_初始化。 **DriverEntry**必须为\_数据结构中的所有成员提供零个\_初始化，然后将其初始化为适用于微型端口驱动程序支持的 HBA 的值。

**DriverEntry**应将**HwInitializationDataSize**成员设置为**sizeof**（HW\_初始化\_数据），以指示该结构使用的是哪个版本的结构，并为其HBA。

接下来， **DriverEntry**调用**ScsiPortInitialize**。 如果微型端口驱动程序支持可连接到多种类型 i/o 总线（例如**MicroChannel**和**Isa**类型总线）的 HBA，则它应为每种类型的 i/o 总线调用**ScsiPortInitialize**一次。 此类微型端口驱动程序必须从**DriverEntry**例程返回对**ScsiPortInitialize**的调用返回的最小值。 小型小型驱动程序编写器不会假设**ScsiPortInitialize**返回的值。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[ **\_数据的 HW\_初始化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_hw_initialization_data)

[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))

[**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize)

 

 







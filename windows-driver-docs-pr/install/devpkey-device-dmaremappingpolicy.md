---
title: DEVPKEY_Device_DmaRemappingPolicy
description: DEVPKEY_Device_DmaRemappingPolicy
ms.assetid: 3553debf-dec8-4135-9bd7-6ce2941afa52
keywords:
- DEVPKEY_Device_DmaRemappingPolicy 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DmaRemappingPolicy
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 07/15/2020
ms.openlocfilehash: db8b9131e0fd2b8afb45895ce555584af2ceb03e
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717070"
---
# <a name="devpkey_device_dmaremappingpolicy"></a>DEVPKEY_Device_DmaRemappingPolicy

DEVPKEY_Device_DmaRemappingPolicy 设备属性的值指示设备的 DMA 重新映射功能。

**属性键**： DEVPKEY_Device_DmaRemappingPolicy  
**属性数据类型标识符**： [ **DEVPROP_TYPE_INT32**](devprop-type-int32.md)  
**属性访问**：应用程序和服务的只读访问。  
已**本地化？**：否  

 
<a name="remarks"></a>备注
-------

| 值 | 含义 |
| ----- | ------- |
| 2     | 此设备上的驱动程序可以使用 DMA 重新映射。 |
| 1     | 此设备上至少有一个驱动程序选择退出 DMA 重新映射。 |
| 0或 DMA 重新映射策略属性不可见 | INF 文件中未指定 DMA 重新映射 INF 指令。 不会为此设备强制执行 DMA 重新映射。 |


可以通过调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 和 [**SetupDiSetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)访问 DEVPKEY_Device_DmaRemappingPolicy 属性。

<a name="requirements"></a>要求
------------

**版本**：在 Windows 10 中提供，版本 1803 (Redstone 4)   
**标头**： Devpkey (包含 Devpkey)   


## <a name="see-also"></a>请参阅

[为设备驱动程序启用 DMA 重新映射](../pci/enabling-dma-remapping-for-device-drivers.md)

[内核 DMA 保护](/windows/security/information-protection/kernel-dma-protection-for-thunderbolt)

[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiSetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)
---
title: DEVPKEY_Device_DmaRemappingPolicy
description: DEVPKEY_Device_DmaRemappingPolicy
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
ms.openlocfilehash: 9ecf372d9b1e035f3275fb81f89018a3a1b826e8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829929"
---
# <a name="devpkey_device_dmaremappingpolicy"></a>DEVPKEY_Device_DmaRemappingPolicy

DEVPKEY_Device_DmaRemappingPolicy 设备属性的值指示设备的 DMA 重新映射功能。

**属性键**： DEVPKEY_Device_DmaRemappingPolicy  
**属性数据类型标识符**： [ **DEVPROP_TYPE_INT32**](devprop-type-int32.md)  
**属性访问**：应用程序和服务的只读访问。  
已 **本地化？**：否  

 
<a name="remarks"></a>备注
-------

| “值” | 含义 |
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

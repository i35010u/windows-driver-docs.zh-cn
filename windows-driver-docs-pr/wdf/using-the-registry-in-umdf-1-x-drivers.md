---
title: 在 UMDF 1.x 驱动程序中使用注册表
description: 在 UMDF 1.x 驱动程序中使用注册表
keywords:
- 注册表 WDK UMDF
- 属性存储对象 WDK UMDF
- UMDF 驱动程序 WDK UMDF，注册表
- 用户模式驱动程序 WDK UMDF、注册表
- UMDF WDK，注册表
- User-Mode Driver Framework WDK，注册表
- 密钥 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddaa8c73a04ceae9158c2fe1c44910a001f32b5d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827381"
---
# <a name="using-the-registry-in-umdf-1x-drivers"></a>在 UMDF 1.x 驱动程序中使用注册表


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

基于 UMDF 的驱动程序可以通过使用属性存储对象的接口来读取和写入注册表中的值。

基于 UMDF 的驱动程序可以访问四种类型的注册表项。 驱动程序可以在这些项下创建、读取和写入子项和值。 以下类型的注册表项可用于基于 UMDF 的驱动程序：

- 硬件密钥

  PnP 管理器将为每个设备创建一个硬件密钥或 *设备密钥*，在该设备中存储设备的唯一标识信息。

  驱动程序可以检索和修改硬件密钥下的某些属性值。 存储值的位置取决于用于访问这些值的方法。

  使用 PropertyStore 方法创建的属性值存储在硬件密钥下的 **\\ 设备参数** 子项中。 若要访问这些属性，驱动程序将调用以下方法之一来获取属性存储接口。

  <a href="" id="iwdfdevice--retrievedevicepropertystore"></a>[**IWDFDevice::RetrieveDevicePropertyStore**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-retrievedevicepropertystore)  
  获取指向 [**IWDFNamedPropertyStore**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfnamedpropertystore) 接口的指针。

  <a href="" id="iwdfdeviceinitialize--retrievedevicepropertystore"></a>[**IWDFDeviceInitialize::RetrieveDevicePropertyStore**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-retrievedevicepropertystore)  
  获取指向 [**IWDFNamedPropertyStore**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfnamedpropertystore) 接口的指针。

  <a href="" id="iwdfpropertystorefactory--retrievedevicepropertystore"></a>[**IWDFPropertyStoreFactory::RetrieveDevicePropertyStore**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfpropertystorefactory-retrievedevicepropertystore)  
  获取指向 [**IWDFNamedPropertyStore2**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfnamedpropertystore2) 接口的指针。 你可以使用 *SubkeyPath* 参数来指定驱动程序创建的子项（如 **\\ Device Parameters \\**<em>DriverServiceName \\ 子项</em>）下的值。

  驱动程序对 **\\ 设备参数** 子项内的值具有只读访问权限，并且无法访问 **\\ 设备参数 \\ WDF** 或 **\\ 设备参数 \\ WUDF**。

  使用统一设备属性模型创建的属性值存储在 " **\\ 属性**" 子项中的 "硬件" 键下。

  若要访问这些属性，驱动程序将调用 [**IWDFUnifiedPropertyStoreFactory：： RetrieveUnifiedDevicePropertyStore**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfunifiedpropertystorefactory-retrieveunifieddevicepropertystore) 以获取属性存储接口。 然后，驱动程序可以使用 [**IWDFUnifiedPropertyStore**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfunifiedpropertystore) 接口来修改和检索设备属性的当前设置。

- 软件密钥

  驱动程序的软件密钥也称为其 *驱动程序密钥* ，因为注册表包含每个驱动程序的软件密钥。 注册表包含所有设备类的列表，每个驱动程序的软件密钥位于其设备类条目下。 系统在其软件密钥下存储有关每个驱动程序的信息。

  你的驱动程序可以调用 [**IWDFPropertyStoreFactory：： RetrieveDevicePropertyStore**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfpropertystorefactory-retrievedevicepropertystore) 来获取对其软件密钥下的值的读取或写入访问权限。 驱动程序可以读取和写入不与特定设备关联的特定于驱动程序的信息。

- 设备接口密钥

  注册表包含驱动程序已创建的所有 [设备接口类](../install/overview-of-device-interface-classes.md) 的键。 其中每个项都是驱动程序已注册的设备接口类的每个实例的条目。

  如果你的驱动程序注册了设备接口类的实例，则它可以通过调用 [**IWDFPropertyStoreFactory：： RetrieveDevicePropertyStore**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfpropertystorefactory-retrievedevicepropertystore)在注册表项的注册表项下读取和写入值。 驱动程序可以读取和写入有关设备接口的实例特定信息。

- **DEVICEMAP** 键

  注册表包含一个 **HKEY 的 \_ 本地 \_ 计算机 \\ 硬件 \\ DEVICEMAP** 密钥，适用于较旧技术（例如串行和并行端口）的驱动程序使用。 如果你的驱动程序支持使用 **DEVICEMAP** 键的技术，则驱动程序可以通过调用 [**IWDFPropertyStoreFactory：： RetrieveDevicePropertyStore**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfpropertystorefactory-retrievedevicepropertystore)访问该键下的子项和值。

驱动程序调用 **RetrieveDevicePropertyStore** 方法之一来打开注册表子项之后，驱动程序可以使用由 [**IWDFNamedPropertyStore**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfnamedpropertystore)、 [**IWDFNamedPropertyStore2**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfnamedpropertystore2)或 [**IWDFUnifiedPropertyStore**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfunifiedpropertystore) 公开的方法来创建、读取和写入子项下的值。 **IWDFNamedPropertyStore2** 接口还允许驱动程序删除值。

有关驱动程序的注册表项的详细信息，请参阅 [注册表树和密钥概述](../install/overview-of-registry-trees-and-keys.md)。

 


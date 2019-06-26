---
title: 在 UMDF 1.x 驱动程序中使用注册表
description: 在 UMDF 1.x 驱动程序中使用注册表
ms.assetid: 653f996a-9fc8-461f-b284-a5d6795259d6
keywords:
- 注册表 WDK UMDF
- 属性存储区对象 WDK UMDF
- UMDF 驱动程序 WDK UMDF、 注册表
- 用户模式驱动程序 WDK UMDF、 注册表
- UMDF WDK 注册表
- 用户模式驱动程序框架 WDK、 注册表
- 密钥 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fc6e8c73ad244a6eb18f2177de8f2d0581c4698
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372192"
---
# <a name="using-the-registry-in-umdf-1x-drivers"></a>在 UMDF 1.x 驱动程序中使用注册表


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

基于 UMDF 驱动程序可以读取和写入注册表中的值，通过使用接口的属性存储对象。

基于 UMDF 驱动程序可以访问四种类型的注册表项。 驱动程序可以创建、 读取和写入子项和这些项下的值。 以下类型的注册表项可供基于 UMDF 驱动程序：

- 硬件密钥

  PnP 管理器创建的硬件密钥，或*设备密钥*，对于每个设备，它将在其中存储设备的唯一标识信息。

  您的驱动程序可以检索和修改某些下的硬件密钥的属性值。 存储的值的位置取决于用于对其进行访问的方法。

  使用 PropertyStore 方法创建的属性值存储在 **\\设备参数** 子项，请在硬件密钥下。 若要访问这些属性，您的驱动程序调用以下方法来获取属性存储区接口之一。

  <a href="" id="iwdfdevice--retrievedevicepropertystore"></a>[**IWDFDevice::RetrieveDevicePropertyStore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-retrievedevicepropertystore)  
  获取指向的指针[ **IWDFNamedPropertyStore** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfnamedpropertystore)接口。

  <a href="" id="iwdfdeviceinitialize--retrievedevicepropertystore"></a>[**IWDFDeviceInitialize::RetrieveDevicePropertyStore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize-retrievedevicepropertystore)  
  获取指向的指针[ **IWDFNamedPropertyStore** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfnamedpropertystore)接口。

  <a href="" id="iwdfpropertystorefactory--retrievedevicepropertystore"></a>[**IWDFPropertyStoreFactory::RetrieveDevicePropertyStore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfpropertystorefactory-retrievedevicepropertystore)  
  获取指向的指针[ **IWDFNamedPropertyStore2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfnamedpropertystore2)接口。 可以使用*SubkeyPath*参数来指定驱动程序创建的子项中的值，如 **\\设备参数\\** <em>DriverServiceName\\子项</em>。

  驱动程序必须为中值的只读访问权限 **\\设备参数** 子项，并且不能访问 **\\设备参数\\WDF** 或 **\\设备参数\\WUDF**。

  使用统一的设备属性模型创建的属性值存储在 **\\属性** 子项，请在硬件密钥下。

  若要访问这些属性，驱动程序调用[ **IWDFUnifiedPropertyStoreFactory::RetrieveUnifiedDevicePropertyStore** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfunifiedpropertystorefactory-retrieveunifieddevicepropertystore)获取属性存储区接口。 然后，可以使用该驱动程序[ **IWDFUnifiedPropertyStore** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfunifiedpropertystore)界面，用于修改和检索设备属性的当前设置。

- 软件密钥

  也称为驱动程序的软件密钥及其*驱动程序键*因为注册表包含软件密钥的每个驱动程序。 注册表包含的所有设备类列表和每个驱动程序软件密钥驻留在其设备类项下。 系统将存储在其软件项下每个驱动程序有关的信息。

  您的驱动程序可以调用[ **IWDFPropertyStoreFactory::RetrieveDevicePropertyStore** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfpropertystorefactory-retrievedevicepropertystore)获取读取或写入访问权限及其软件项下的值。 该驱动程序可以读取和写入不是与特定设备关联的特定于驱动程序的信息。

- 设备接口密钥

  注册表包含键的所有[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)驱动程序已创建。 在每个项是为每个驱动程序已注册的设备接口类实例的条目。

  如果您的驱动程序已注册设备接口类的实例，它可以读取和写入该实例的注册表项之下的值通过调用[ **IWDFPropertyStoreFactory::RetrieveDevicePropertyStore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfpropertystorefactory-retrievedevicepropertystore). 该驱动程序可以读取和写入设备接口的特定于实例的信息。

- **DEVICEMAP**密钥

  注册表包含**HKEY\_本地\_机\\硬件\\DEVICEMAP**旧技术，如串行和并行端口，某些驱动程序使用的密钥。 如果您的驱动程序支持使用的技术**DEVICEMAP**键，该驱动程序可以访问子项和项下的值通过调用[ **IWDFPropertyStoreFactory::RetrieveDevicePropertyStore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfpropertystorefactory-retrievedevicepropertystore).

驱动程序已调用之一后**RetrieveDevicePropertyStore**方法以打开注册表子项，则驱动程序可使用公开的方法[ **IWDFNamedPropertyStore** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfnamedpropertystore)[ **IWDFNamedPropertyStore2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfnamedpropertystore2)，或[ **IWDFUnifiedPropertyStore** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfunifiedpropertystore)来创建、 读取和写入下的值子项。 **IWDFNamedPropertyStore2**接口还允许驱动程序，以删除值。

有关驱动程序的注册表项的详细信息，请参阅[概述的注册表树和密钥](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-registry-trees-and-keys)。

 

 






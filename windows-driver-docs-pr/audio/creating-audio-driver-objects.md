---
title: 创建音频驱动程序对象
description: 创建音频驱动程序对象
ms.assetid: c5d1b1b6-fc47-4227-bcca-1119488dce3b
keywords:
- 音频驱动程序对象 WDK
- COM 对象创建 WDK 音频
- 对象 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c95e9e75b0c49d6c3d1d4d42636e94e7f2b3c0d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833585"
---
# <a name="creating-audio-driver-objects"></a>创建音频驱动程序对象


## <span id="creating_audio_driver_objects"></span><span id="CREATING_AUDIO_DRIVER_OBJECTS"></span>


在用户模式下，COM 对象是使用一个**函数（如**Microsoft Windows SDK 文档中所述）创建的，其中客户端不知道如何分配对象的内存。 但是，在内核模式下，内存分配往往受到严格控制，需要创建不同的对象创建方法。

音频驱动程序模型使用由**IUnknown**接口定义的 COM 接口的概念。 但是，音频驱动程序不需要访问注册表或使用进程内服务器等机制。 无需微型端口驱动程序即可支持聚合。

按照约定，用于创建特定对象类的函数始终采用相同的形式：

```cpp
NTSTATUS CreateMyObject(
   OUT PUNKNOWN  *Unknown,
   IN REFGUID ClassId,
   IN PUNKNOWN OuterUnknown OPTIONAL,
   IN POOL_TYPE PoolType
 );
```

### <a name="span-idparametersspanspan-idparametersspanparameters"></a><span id="parameters"></span><span id="PARAMETERS"></span>Parameters

<span id="Unknown"></span><span id="unknown"></span><span id="UNKNOWN"></span>*未知*  
指向**IUnknown**接口的指针的指针。 函数通过*Unknown*输出对新创建的对象的引用。

<span id="ClassId"></span><span id="classid"></span><span id="CLASSID"></span>*ClassId*  
指定通过引用传递的类 GUID。 仅当函数创建多个类的对象时，才使用此参数。 否则，将其设置为**NULL**。

<span id="OuterUnknown"></span><span id="outerunknown"></span><span id="OUTERUNKNOWN"></span>*OuterUnknown*  
指定用于聚合新对象的**IUnknown**接口。 可以将此参数设置为**NULL** ，以指示不需要聚合。

<span id="PoolType"></span><span id="pooltype"></span><span id="POOLTYPE"></span>*PoolType*  
指定要从中分配对象的内存池的类型（请参阅[**池\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_pool_type)）。

前三个参数与 COM **CoCreateInstance**函数的参数相同。 有关此类型的创建函数的示例，请参阅 Microsoft Windows 驱动程序工具包（WDK）中的 Fmsynth 示例音频驱动程序中的**CreateMiniportMidiFM**函数。

另一种约定是为类提供新的*Xxx*函数。 此类函数提供了一种简单的方法来实例化（创建和初始化）对象，如下面的示例中所示：

```cpp
NTSTATUS NewMyObject(
 OUT PMYINTERFACE  *InterfacePointer,
 IN PUNKNOWN  OuterUnknown OPTIONAL,
 IN POOL_TYPE  PoolType,
  // ...more parameters
 );
```

NewMyObject 函数创建并初始化对象，然后将指针传递回接口。 由于初始化参数是类特定的，因此是新的*Xxx*函数的原型。 新的*Xxx*函数为对象的构造函数提供了方便的访问。

有关此类型的新*Xxx*函数的示例，请参阅[**PcNewDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewdmachannel)。

 

 





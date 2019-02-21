---
title: 创建音频驱动程序对象
description: 创建音频驱动程序对象
ms.assetid: c5d1b1b6-fc47-4227-bcca-1119488dce3b
keywords:
- WDK 的音频驱动程序对象
- COM 对象创建 WDK 音频
- 对象 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f086bce6c2bdc411a8d968bb819892f45fcb0c34
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525791"
---
# <a name="creating-audio-driver-objects"></a>创建音频驱动程序对象


## <span id="creating_audio_driver_objects"></span><span id="CREATING_AUDIO_DRIVER_OBJECTS"></span>


在用户模式下，使用函数类似于创建 COM 对象**CoCreateInstance** （Microsoft Windows SDK 文档中介绍），客户端是不知道如何分配的对象所需的内存。 在内核模式下，但是，其中的内存分配往往会严格控制，对象创建的不同方法是必需的。

音频驱动程序模型定义的使用的 COM 接口，概念**IUnknown**接口。 但是，音频驱动程序，则不需要访问注册表或使用进程内服务器之类的机制。 微型端口驱动程序不需要支持聚合。

按照约定，用来始终创建某类对象的函数采用相同的形式：

```cpp
NTSTATUS CreateMyObject(
   OUT PUNKNOWN  *Unknown,
   IN REFGUID ClassId,
   IN PUNKNOWN OuterUnknown OPTIONAL,
   IN POOL_TYPE PoolType
 );
```

### <a name="span-idparametersspanspan-idparametersspanparameters"></a><span id="parameters"></span><span id="PARAMETERS"></span>参数

<span id="Unknown"></span><span id="unknown"></span><span id="UNKNOWN"></span>*未知*  
指针到指向**IUnknown**接口。 该函数将输出通过新创建的对象的引用*未知*。

<span id="ClassId"></span><span id="classid"></span><span id="CLASSID"></span>*ClassId*  
指定的类由引用传递的 GUID。 该函数将创建的多个类的对象时，才使用此参数。 否则，设置为**NULL**。

<span id="OuterUnknown"></span><span id="outerunknown"></span><span id="OUTERUNKNOWN"></span>*OuterUnknown*  
指定**IUnknown**用于聚合的新对象的接口。 此参数可以设置为**NULL**以不指示任何聚合都不需要。

<span id="PoolType"></span><span id="pooltype"></span><span id="POOLTYPE"></span>*PoolType*  
指定是要分配对象的内存池的类型 (请参阅[**池\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff559707))。

前三个参数是等同于 COM 参数**CoCreateInstance**函数。 有关此类型的创建函数的示例，请参阅**CreateMiniportMidiFM** Fmsynth 示例音频驱动程序中 Microsoft Windows Driver Kit (WDK) 中的函数。

另一个惯例是提供新*Xxx*类的函数。 此类函数可以方便地实例化 （创建和初始化） 对象，如下面的示例中所示：

```cpp
NTSTATUS NewMyObject(
 OUT PMYINTERFACE  *InterfacePointer,
 IN PUNKNOWN  OuterUnknown OPTIONAL,
 IN POOL_TYPE  PoolType,
  // ...more parameters
 );
```

NewMyObject 函数创建和初始化对象，然后将指针传递到的接口。 由于初始化参数都特定于类，因此是新的原型*Xxx*函数。 新建*Xxx*函数提供了对对象构造函数的便捷访问。

有关新的示例*Xxx*函数的这种类型，请参阅[ **PcNewDmaChannel**](https://msdn.microsoft.com/library/windows/hardware/ff537712)。

 

 




